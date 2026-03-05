### match
```
...
 namespace sandbox::policy::features { ... 
 bool IsNetworkSandboxEnabled() { ... 
// BUILDFLAG(IS_MAC) || BUILDFLAG(IS_FUCHSIA)
 } 
 >>> 
 ... } ...  
```
### patch
```
BASE_FEATURE(kModuleFileNamePatch,
             base::FEATURE_DISABLED_BY_DEFAULT);

```

