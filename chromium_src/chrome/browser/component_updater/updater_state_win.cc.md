### match
```
...
 namespace component_updater { ... 
 namespace { ... 
const wchar_t kRegValueLastStartedAU[] = L"LastStartedAU";
 const wchar_t kRegValueLastChecked[] = L"LastChecked"; 
 >>> 
base::Time GetUpdaterTimeValue(bool is_machine, const wchar_t* value_name) {
  const HKEY root_key = is_machine ? HKEY_LOCAL_MACHINE : HKEY_CURRENT_USER;
  base::win::RegKey update_key;

  if (update_key.Open(root_key, kRegPathGoogleUpdate,
                      KEY_QUERY_VALUE | KEY_WOW64_32KEY) == ERROR_SUCCESS) {
    DWORD value(0);
    if (update_key.ReadValueDW(value_name, &value) == ERROR_SUCCESS) {
      return base::Time::FromTimeT(value);
    }
  }

  return base::Time();
}
 ... } ...  } ...  
```
### patch
```
// Brave Update group policy settings.
const wchar_t kGoogleUpdatePoliciesKey[] =
    L"SOFTWARE\\Policies\\BraveSoftware\\Update";
const wchar_t kCheckPeriodOverrideMinutes[] = L"AutoUpdateCheckPeriodMinutes";
const wchar_t kUpdatePolicyValue[] = L"UpdateDefault";
#if BUILDFLAG(IS_BRAVE_ORIGIN_BRANDED)
const wchar_t kChromeUpdatePolicyOverride[] =
    L"Update{F1EF32DE-F987-4289-81D2-6C4780027F9B}";
#else
const wchar_t kChromeUpdatePolicyOverride[] =
    L"Update{AFE6A462-C574-4B8A-AF43-4CC60DF4563B}";
#endif  // BUILDFLAG(IS_BRAVE_ORIGIN_BRANDED)

// Don't allow update periods longer than six weeks (Chrome release cadence).
const int kCheckPeriodOverrideMinutesMax = 60 * 24 * 7 * 6;

// Brave Update registry settings.
const wchar_t kRegPathGoogleUpdate[] = L"Software\\BraveSoftware\\Update";
const wchar_t kRegPathClientsGoogleUpdate[] =
    L"Software\\BraveSoftware\\Update\\Clients\\"
    L"{B131C935-9BE6-41DA-9599-1F776BEB8019}";


```

