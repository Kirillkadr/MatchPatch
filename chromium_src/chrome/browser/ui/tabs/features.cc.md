### match
```cpp
...
 
 namespace tabs { ... 
// newly opened tab to close that tab and return focus to the opener tab.
 BASE_FEATURE(kBackToOpener, base::FEATURE_DISABLED_BY_DEFAULT); 
 >>> 
bool IsVerticalTabsFeatureEnabled() {
  return base::FeatureList::IsEnabled(kVerticalTabs) ||
         base::FeatureList::IsEnabled(kVerticalTabsLaunch);
  ;
}
 ... } ...  
```
### patch
```cpp
#if BUILDFLAG(IS_LINUX)
BASE_FEATURE(kBraveChangeActiveTabOnScrollEvent,
             base::FEATURE_ENABLED_BY_DEFAULT);
#endif  // BUILDFLAG(IS_LINUX)

BASE_FEATURE(kBraveSharedPinnedTabs, base::FEATURE_DISABLED_BY_DEFAULT);

BASE_FEATURE(kBraveHorizontalTabsUpdate, base::FEATURE_ENABLED_BY_DEFAULT);

BASE_FEATURE(kBraveCompactHorizontalTabs, base::FEATURE_DISABLED_BY_DEFAULT);

BASE_FEATURE(kBraveVerticalTabScrollBar, base::FEATURE_DISABLED_BY_DEFAULT);

BASE_FEATURE(kBraveVerticalTabHideCompletely, base::FEATURE_ENABLED_BY_DEFAULT);

BASE_FEATURE(kBraveTreeTab, base::FEATURE_DISABLED_BY_DEFAULT);

bool HorizontalTabsUpdateEnabled() {
  return base::FeatureList::IsEnabled(kBraveHorizontalTabsUpdate);
}


```

