### match
```cpp
...
// Updates the pin button.
>>> 
 void UpdatePinButton(bool is_force_pinned, bool is_pinned); 
<<< 
...
```
### patch
```cpp
  virtual void UpdatePinButton(bool is_force_pinned, bool is_pinned);

```

### match
```cpp
...
 
 class ExtensionMenuItemView : public views::FlexLayoutView,
                              public ExtensionContextMenuController::Observer { ... 
// Handles the pin button press. This is passed as a callback to
 // `pin_button_`. 
 >>> 
 ... } ...  
```
### patch
```cpp
  friend class BraveExtensionMenuItemView;

```

