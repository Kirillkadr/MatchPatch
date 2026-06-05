### match
```cpp
...
 
 namespace privacy_sandbox { ... 
// the Ad API prefs to it's default value.
 void MaybeClearAdPrivacyPrefs(PrefService* pref_service); 
 >>> 
 ... } ...  
```
### patch
```cpp
// The following prefs have been deprecated and privated, however in Brave it
// is necessary to keep these prefs visible while they are deprecated to make
// sure these modes are not enabled.
inline constexpr char kPrivacySandboxManuallyControlledV2[] =
    "privacy_sandbox.manually_controlled_v2";

```

