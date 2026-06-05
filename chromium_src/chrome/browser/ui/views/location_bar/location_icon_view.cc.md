### match
```cpp
...
 
 void LocationIconView::UpdateBackground() { ... 
 SetBackgroundColor(GetColorProvider()->GetColor(id)); 
 >>> 
 ... } ...  
```
### patch
```cpp
  return;

```

