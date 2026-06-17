### match
```cpp
...
 
 namespace { ... 
 
 class MdIPHBubbleButton : public views::MdTextButton { ... 
 ~MdIPHBubbleButton() override = default; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  void UpdateTextColor() override {} 

```

