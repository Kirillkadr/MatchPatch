### match
```
...
#include <stddef.h>

 #include <map>
 
 >>> 
#include "base/check.h"

 ... 
```
### patch
```
#include "base/feature_list.h"
#include "brave/sandbox/win/src/module_file_name_interception.h"

```

### match
```
...
// This code executes on the broker side, as a callback from the policy on the
 // target side (the child). 
 >>> 
namespace sandbox {

bool SetupNtdllImports(TargetProcess& child) {
  return (SBOX_ALL_OK ==
          child.TransferVariable(GetNtExports(),
                                 const_cast<NtExports*>(GetNtExports()),
                                 sizeof(NtExports)));
}

#undef INIT_GLOBAL_NT
#undef INIT_GLOBAL_RTL

bool SetupBasicInterceptions(InterceptionManager* manager,
                             bool is_csrss_connected) {
  // Interceptions provided by process_thread_policy, without actual policy.
  if (!INTERCEPT_NT(manager, NtOpenThread, OPEN_THREAD_ID, 20) ||
      !INTERCEPT_NT(manager, NtOpenProcess, OPEN_PROCESS_ID, 20) ||
      !INTERCEPT_NT(manager, NtOpenProcessToken, OPEN_PROCESS_TOKEN_ID, 16))
    return false;

  // Interceptions with neither policy nor IPC.
  if (!INTERCEPT_NT(manager, NtSetInformationThread, SET_INFORMATION_THREAD_ID,
                    20) ||
      !INTERCEPT_NT(manager, NtOpenThreadToken, OPEN_THREAD_TOKEN_ID, 20))
    return false;

  // This one is also provided by process_thread_policy.
  if (!INTERCEPT_NT(manager, NtOpenProcessTokenEx, OPEN_PROCESS_TOKEN_EX_ID,
                    20))
    return false;

  if (!INTERCEPT_NT(manager, NtOpenThreadTokenEx, OPEN_THREAD_TOKEN_EX_ID, 24))
    return false;

  if (!is_csrss_connected) {
    if (!INTERCEPT_EAT(manager, kKerneldllName, CreateThread, CREATE_THREAD_ID,
                       28))
      return false;
  }

  return true;
}

}
 ... 
```
### patch
```
#if !defined(PSAPI_VERSION)
#error <Psapi.h> should be included.
#endif

```

### match
```
...
>>>
 bool 
 SetupBasicInterceptions 
 ( 
 InterceptionManager* manager 
 ,  <<< ... 
bool is_csrss_connected
 ... ) ...  
```
### patch
```
bool SetupBasicInterceptions_ChromiumImpl(InterceptionManager* manager,

```

### match
```
...
 namespace sandbox { ... 
 bool SetupBasicInterceptions_ChromiumImpl(InterceptionManager* manager,
bool is_csrss_connected) { ... 
return true;
 } 
 >>> 
 ... } ...  
```
### patch
```
namespace {
bool SetupModuleFilenameInterceptions(InterceptionManager* manager,
                                      const TargetConfig* config) {
  if (!config->ShouldPatchModuleFileName()) {
    return true;
  }

  if (!INTERCEPT_EAT(manager, kKerneldllName, GetModuleFileNameA,
                     GET_MODULE_FILENAME_A_ID, 3)) {
    return false;
  }

#if !defined(ADDRESS_SANITIZER)
  // This function is called too early in ASAN initialization.
  if (!INTERCEPT_EAT(manager, kKerneldllName, GetModuleFileNameW,
                     GET_MODULE_FILENAME_W_ID, 3)) {
    return false;
  }
#endif

#if (PSAPI_VERSION > 1)
  if (!INTERCEPT_EAT(manager, kKerneldllName, K32GetModuleFileNameExA,
                     GET_MODULE_FILENAME_EX_A_ID, 4)) {
    return false;
  }
  if (!INTERCEPT_EAT(manager, kKerneldllName, K32GetModuleFileNameExW,
                     GET_MODULE_FILENAME_EX_W_ID, 4)) {
    return false;
  }
#else
  if (!INTERCEPT_EAT(manager, kKerneldllName, GetModuleFileNameExA,
                     GET_MODULE_FILENAME_EX_A_ID, 4)) {
    return false;
  }
  if (!INTERCEPT_EAT(manager, kKerneldllName, GetModuleFileNameExW,
                     GET_MODULE_FILENAME_EX_W_ID, 4)) {
    return false;
  }
#endif
  return true;
}
}  // namespace

bool SetupBasicInterceptions(InterceptionManager* manager,
                             bool is_csrss_connected,
                             const TargetConfig* config) {
  if (!SetupBasicInterceptions_ChromiumImpl(manager, is_csrss_connected)) {
    return false;
  }

  if (!SetupModuleFilenameInterceptions(manager, config)) {
    return false;
  }

  return true;
}

```

