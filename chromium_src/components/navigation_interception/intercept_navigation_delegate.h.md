### match
```cpp
...
 
 # ifndef ... 
 
 namespace navigation_interception { ... 
 
 class InterceptNavigationDelegate : public base::SupportsUserData::Data { ...   >>> 
 void 
 ShouldIgnoreNavigation 
 (  <<< 
content::NavigationHandle* navigation_handle
 ... ) ...  } ...  } ...  
```
### patch
```cpp
  void virtual ShouldIgnoreNavigation(

```

