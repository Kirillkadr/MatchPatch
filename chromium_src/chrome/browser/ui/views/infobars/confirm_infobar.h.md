### match
```cpp
...
 
 class ConfirmInfoBar : public InfoBarView { ... 
 views::MdTextButton* cancel_button_for_testing() { return cancel_button_; } 
 >>> 
 ... } ...  
```
### patch
```cpp
  friend class BraveSyncAccountDeletedInfoBar;
  friend class BraveConfirmInfoBar;

```

