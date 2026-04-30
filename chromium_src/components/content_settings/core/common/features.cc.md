### match
```cpp
...
 
 // namespace features 
 >>> 
...
```
### patch
```cpp

namespace features {

OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kTrackingProtection3pcd, base::FEATURE_DISABLED_BY_DEFAULT},
    {kUserBypassUI, base::FEATURE_DISABLED_BY_DEFAULT},
}});

}  // namespace features

// Brave implements a strictier policy to not leak blocked permissions into
// incognito profiles. This feature (when enabled) restores the original
// Chromium implementation which makes INHERIT_IF_LESS_PERMISSIVE inherit
// blocked permissions in incognito profile.
BASE_FEATURE(kAllowIncognitoPermissionInheritance,
             base::FEATURE_DISABLED_BY_DEFAULT);
```

