### match
```cpp

...
 namespace sandbox::policy::features { ... 
 bool IsNetworkSandboxEnabled() { ... 
// BUILDFLAG(IS_MAC) || BUILDFLAG(IS_FUCHSIA)
 } 
 >>> 
 ... } ...  
```
### patch
```cpp

BASE_FEATURE(kModuleFileNamePatch,
             base::FEATURE_DISABLED_BY_DEFAULT);

```

