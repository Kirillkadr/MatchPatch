### match
```cpp
...
 
 class SystemMenuModelDelegate : public ui::SimpleMenuModel::Delegate { ... 
 // Overridden from ui::SimpleMenuModel::Delegate: 
 >>> 
 ... } ...  
```
### patch
```cpp
  bool IsCommandIdChecked_ChromiumImpl(int command_id) const;

```

### match
```cpp
...
 bool IsItemForCommandIdDynamic(int command_id) const override; 
 >>> 
 ... 
```
### patch
```cpp
  std::u16string GetLabelForCommandId_ChromiumImpl(int command_id) const; 

```

