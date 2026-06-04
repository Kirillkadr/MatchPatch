### match
```cpp
...
 
 # ifndef ... 
 
 class ConfirmInfoBarDelegate : public infobars::InfoBarDelegate { ... 
 
 enum InfoBarButton { ... 
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
#if !BUILDFLAG(IS_IOS) && !BUILDFLAG(IS_ANDROID)
class ConfirmInfoBarDelegate : public infobars::InfoBarDelegate {
 public:
  enum InfoBarButton {
    BUTTON_NONE = 0,
    BUTTON_OK = 1 << 0,
    BUTTON_EXTRA = 1 << 2, BUTTON_CANCEL,
   };
#endif

```

