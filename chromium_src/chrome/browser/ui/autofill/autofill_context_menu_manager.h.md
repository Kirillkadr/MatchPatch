### match
```cpp
...
 
 # ifndef ... 
 
 namespace autofill { ... 
 
 class AutofillContextMenuManager : public RenderViewContextMenuObserver { ... 
// Autofill context menu entries are conditioned on
 // `ContextMenuContentType::ITEM_GROUP_AUTOFILL`. 
 >>> 
void AppendItems();
 ... } ...  } ...  
```
### patch
```cpp
  void AppendItems_ChromiumImpl(); 

```

