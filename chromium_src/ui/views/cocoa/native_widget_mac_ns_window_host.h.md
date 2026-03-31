### match
```cpp

...
 # ifndef ... 
 namespace views { ... 
// Called when the owning Widget's Init method has completed.  >>> 
 void OnWidgetInitDone();  <<< ... 
// Redispatch a keyboard event using the widget's window's CommandDispatcher.
 ... } ...  
```
### patch
```cpp

  void SetWindowTitleVisibility(bool visible); 
  void OnWidgetInitDone

```

