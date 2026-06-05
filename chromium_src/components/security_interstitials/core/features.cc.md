### match
```cpp
...
 
 namespace security_interstitials::features { ... 
 
 BASE_FEATURE ( ... 
kInsecureFormNavigationThrottleForPrerender,
             
 base::FEATURE_ENABLED_BY_DEFAULT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
#if BUILDFLAG(IS_ANDROID)
OVERRIDE_FEATURE_DEFAULT_STATES({{
    // Disable dialog UI on Android since Android doesn't have the dialog
    // implementation and should use the full-page interstitial instead.
    {kHttpsFirstDialogUi, base::FEATURE_DISABLED_BY_DEFAULT},
}});
#endif

```

