### match
```cpp
...
 
bool IsFluidResizeEnabled() {
  // On phones, resizes are almost exclusively discrete transitions, such as
  // orientation swaps. For these events, the standard immediate synchronization
  // path is more efficient and results in fewer artifacts.
  // By contrast, the continuous resize logic is optimized for the "live" window
  // dragging seen on tablets and desktops.
  return base::FeatureList::IsEnabled(features::kFluidResize) &&
         (base::android::device_info::is_tablet() ||
          base::android::device_info::is_desktop());
}
 #endif 
 >>> 
 ...
```
### patch
```cpp
// This is intended as a kill switch for the Idle Detection feature. To enable
// this feature, the experimental web platform features flag should be set,
// or the site should obtain an Origin Trial token.
BASE_FEATURE(kIdleDetection, base::FEATURE_DISABLED_BY_DEFAULT);
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kDevToolsPrivacyUI, base::FEATURE_DISABLED_BY_DEFAULT},
    {kDigitalGoodsApi, base::FEATURE_DISABLED_BY_DEFAULT},
    {kFedCm, base::FEATURE_DISABLED_BY_DEFAULT},
    {kPrefetchProxy, base::FEATURE_DISABLED_BY_DEFAULT},
    {kPrivacySandboxAdsAPIsOverride, base::FEATURE_DISABLED_BY_DEFAULT},
    {kServiceWorkerAutoPreload, base::FEATURE_DISABLED_BY_DEFAULT},
    {kWebIdentityDigitalCredentials, base::FEATURE_DISABLED_BY_DEFAULT},
    {kWebIdentityDigitalCredentialsCreation, base::FEATURE_DISABLED_BY_DEFAULT},
#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_MAC) || BUILDFLAG(IS_LINUX)
    {kPwaNavigationCapturing, base::FEATURE_DISABLED_BY_DEFAULT},
#endif
    {kWebOTP, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

