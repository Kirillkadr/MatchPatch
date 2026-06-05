### match
```cpp
...
 
 namespace tab_groups { ... 
void SetTextProperties(const SavedTabGroup& group);
>>> 
 void UpdateButtonLayout(); 
<<< 
void UpdateAccessibleName();
 ... } ...  
```
### patch
```cpp
  friend class BraveSavedTabGroupButton; 
  virtual void UpdateButtonLayout();

```

