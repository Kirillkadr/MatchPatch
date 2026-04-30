### match
```cpp
...

 BASE_FEATURE(kYourSavedInfoSettingsPage, base::FEATURE_DISABLED_BY_DEFAULT); 
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kAutofillAiServerModel, base::FEATURE_DISABLED_BY_DEFAULT},
#if BUILDFLAG(IS_ANDROID)
    {kAutofillEnableLoyaltyCardsFilling, base::FEATURE_DISABLED_BY_DEFAULT},
#endif  // BUILDFLAG(IS_ANDROID)
}});

```

