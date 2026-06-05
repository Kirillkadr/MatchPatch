### match
```cpp
...
 
 class ChromeLocationBarModelDelegate : public LocationBarModelDelegate { ... 
~ChromeLocationBarModelDelegate() override;
 // Helper method to get the navigation entry from the navigation controller. 
 >>> 
content::NavigationEntry* GetNavigationEntry() const;
 ... } ...  
```
### patch
```cpp
  friend class BraveLocationBarModelDelegate;

```

