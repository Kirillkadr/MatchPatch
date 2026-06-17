### match
```cpp
...
 
 namespace split_tabs { ... 
 std::vector<tabs::TabInterface*> ListTabs() const; 
 >>> 
// Returns the TabCollection handle associated with this split.
 ... } ...  
```
### patch
```cpp
  bool linked() const {
    return linked_;
  }
  void set_linked(bool linked) {
    linked_ = linked;
  }

 private:
  bool linked_ = false;

 public:
  void UnUsed() const;

```

