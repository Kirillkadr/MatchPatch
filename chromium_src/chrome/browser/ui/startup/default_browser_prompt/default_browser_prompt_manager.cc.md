### match
```cpp
...
 void 
 DefaultBrowserPromptManager::SetAppMenuItemVisibility(bool show) 
 { 
 >>> 
show_app_menu_item_ = show;
 ... } ...  
```
### patch
```cpp
  if (show) {                    
    show_app_menu_item_ = false;
    return;
  }

```

