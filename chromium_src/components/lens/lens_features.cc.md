### match
```cpp
...
 
 bool IsLensSendRawFileMediaTypesEnabled() {
  return base::FeatureList::IsEnabled(kLensSendRawFileMediaTypes);
}
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kLensOverlay, base::FEATURE_DISABLED_BY_DEFAULT},
    {kLensOverlayOmniboxEntryPoint, base::FEATURE_DISABLED_BY_DEFAULT},
    {kLensStandalone, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

