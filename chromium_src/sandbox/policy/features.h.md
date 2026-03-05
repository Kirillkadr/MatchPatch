### match
```
...
 # ifndef ... 
 namespace sandbox::policy::features { ... 
// calling ContentBrowserClient::ShouldSandboxNetworkService().
 SANDBOX_POLICY_EXPORT bool IsNetworkSandboxEnabled(); 
 >>> 
 ... } ...  
```
### patch
```
// Enables patching of executable's name from brave.exe to chrome.exe in
// sandboxed processes.
SANDBOX_POLICY_EXPORT BASE_DECLARE_FEATURE(kModuleFileNamePatch);

```

