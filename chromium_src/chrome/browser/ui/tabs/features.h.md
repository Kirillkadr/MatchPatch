### match
```cpp
...
 
 namespace tabs { ... 
BASE_DECLARE_FEATURE(kHorizontalTabStripComboButton);
 BASE_DECLARE_FEATURE_PARAM(bool, kHorizontalTabStripComboButtonShowStartOnly) 
 ; 
 >>> 
bool IsVerticalTabsFeatureEnabled();
 ... } ...  
```
### patch
```cpp
#if BUILDFLAG(IS_LINUX)
// This flag controls the behavior of browser_default::kScrollEventChangesTab,
// which is true only when it's Linux.
BASE_DECLARE_FEATURE(kBraveChangeActiveTabOnScrollEvent);
#endif  // BUILDFLAG(IS_LINUX)

BASE_DECLARE_FEATURE(kBraveSharedPinnedTabs);

BASE_DECLARE_FEATURE(kBraveHorizontalTabsUpdate);

BASE_DECLARE_FEATURE(kBraveCompactHorizontalTabs);

BASE_DECLARE_FEATURE(kBraveVerticalTabScrollBar);

BASE_DECLARE_FEATURE(kBraveVerticalTabHideCompletely);

BASE_DECLARE_FEATURE(kBraveTreeTab);

bool HorizontalTabsUpdateEnabled();



```

