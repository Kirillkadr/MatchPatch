### match
```cpp
...
 
 class ExtensionsMenuEntryView
    : public views::FlexLayoutView,
      public ExtensionContextMenuController::Observer { ... 
>>> 
 void 
 UpdateContextMenuButton 
 ( 
<<< 
...) ...  } ...  
```
### patch
```cpp
  virtual void UpdateContextMenuButton(

```

### match
```cpp
...
 
 class ExtensionsMenuEntryView
    : public views::FlexLayoutView,
      public ExtensionContextMenuController::Observer { ... 
// Sets ups the context menu button controllers. Must be called by the
 // constructor. 
 >>> 
 ... } ...  
```
### patch
```cpp
  friend class BraveExtensionsMenuEntryView;

```

