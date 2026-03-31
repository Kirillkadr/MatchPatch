### match
```cpp
...
 
 # ifndef ... 
 
 namespace feature_engagement { ... 
FEATURE_CONSTANTS_DECLARE_FEATURE(kIPHResumptionRailFeature);
 #endif 
 // !BUILDFLAG(IS_IOS) 
 >>> 
 ... } ...  
```
### patch
```cpp
#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_MAC) || BUILDFLAG(IS_LINUX)
// IPH for notifying users that Brave Shields settings have moved to Page Info.
FEATURE_CONSTANTS_DECLARE_FEATURE(kIPHBraveShieldsInPageInfoFeature);
#endif

```

