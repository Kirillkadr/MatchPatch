### match
```cpp
...
 
 namespace enterprise_signals::features { ... 
 
 BASE_FEATURE ( ... 
kNewEvSignalsUnaffiliatedEnabled,
             
 base::FEATURE_DISABLED_BY_DEFAULT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
#if BUILDFLAG(IS_LINUX) || BUILDFLAG(IS_WIN) || BUILDFLAG(IS_MAC)
    {kDeviceSignalsConsentDialog, base::FEATURE_DISABLED_BY_DEFAULT},
#endif
}});

```

