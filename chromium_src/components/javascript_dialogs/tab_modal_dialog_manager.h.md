### match
```cpp
...
 
 # ifndef ... 
 
 namespace javascript_dialogs { ... 
 
 class TabModalDialogManager
    : public content::JavaScriptDialogManager,
      public content::WebContentsObserver,
      public content::WebContentsUserData<TabModalDialogManager> { ... 
TabModalDialogManager& operator=(const TabModalDialogManager&) = delete;
 ~TabModalDialogManager() override; 
 >>> 
void BrowserActiveStateChanged();
 ... } ...  } ...  
```
### patch
```cpp
  void OnTabActiveStateChanged();      

```

