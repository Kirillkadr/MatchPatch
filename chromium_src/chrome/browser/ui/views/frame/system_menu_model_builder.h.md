### match
```cpp
...
 
 class SystemMenuModelBuilder { ... 
 // Populates the menu. 
 >>> 
 ... } ...  
```
### patch
```cpp

 private:
  friend class BraveSystemMenuModelBuilder;

 public:

```

### match
```cpp
...
>>>
 void BuildSystemMenuForBrowserWindow(ui::SimpleMenuModel* model); 
<<< 
...
```
### patch
```cpp
  virtual void BuildSystemMenuForBrowserWindow(ui::SimpleMenuModel* model);

```

