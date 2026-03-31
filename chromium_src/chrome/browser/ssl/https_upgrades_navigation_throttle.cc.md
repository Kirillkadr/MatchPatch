### match
```cpp
...
 
 namespace { ... 
// more like interstitials.
 inline constexpr char kBlankPageHtml[] = "<html></html>"; 
 >>> 
 ... } ...  
```
### patch
```cpp
// Tor is slow and needs a longer fallback delay
constexpr base::TimeDelta kTorFallbackDelay = base::Seconds(20);

bool IsTor(content::NavigationHandle* handle) {
  auto* context = handle->GetWebContents()->GetBrowserContext();
  Profile* profile = Profile::FromBrowserContext(context);
  return profile->IsTor();
}


```

### match
```cpp
...
 
 content::NavigationThrottle::ThrottleCheckResult
HttpsUpgradesNavigationThrottle::WillRedirectRequest() { ... 
 
 if (tab_helper->is_navigation_upgraded()) { ...   >>> 
 navigation_handle()->SetNavigationTimeout(g_fallback_delay) 
 ;  <<<  ...} ...  } ...  
```
### patch
```cpp
        navigation_handle()->SetNavigationTimeout(IsTor(navigation_handle()) ? kTorFallbackDelay
                                                  :g_fallback_delay);

```

