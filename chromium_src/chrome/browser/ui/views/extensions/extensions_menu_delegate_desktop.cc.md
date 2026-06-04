### match
```cpp
...
 void 
 ExtensionsMenuDelegateDesktop::OpenMainPage() 
 { 
 >>> 
 ... } ...  
```
### patch
```cpp
    {
    auto main_page =
        std::make_unique<BraveExtensionsMenuMainPageView>(browser_, this);
    UpdateMainPage(main_page.get());
    PopulateMainPage(main_page.get());
    SwitchToPage(std::move(main_page));
    return;                                                                
  }

```

