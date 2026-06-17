### match
```cpp
...
 
 namespace tabs { ... 
 size_t IndexOfFirstNonPinnedTab() const; 
 >>> 
 ... } ...  
```
### patch
```cpp
  void virtual AddTabRecursive(std::unique_ptr<TabInterface> tab,
                       size_t index,
                       std::optional<tab_groups::TabGroupId> new_group_id,
                       bool new_pinned_state, TabInterface* opener);

```

### match
```cpp
...
 
 namespace tabs { ... 
 
 class TabStripCollection : public TabCollection { ... 
>>> 
 void 
 MoveTabRecursive 
 ( 
 size_t initial_index 
 , 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
  void virtual MoveTabRecursive(size_t initial_index,

```

### match
```cpp
...
 
 namespace tabs { ... 
 
 class TabStripCollection : public TabCollection { ... 
>>> 
 void 
 MoveTabsRecursive 
 ( 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
  void virtual MoveTabsRecursive(

```

### match
```cpp
...
 
 namespace tabs { ... 
// due to bad input then CHECK.
>>> 
 std::unique_ptr<TabInterface> RemoveTabAtIndexRecursive(size_t index); 
<<< 
// TabCollection:
 ... } ...  
```
### patch
```cpp
  std::unique_ptr<TabInterface> RemoveTabAtIndexRecursive_Chromium(size_t index);
  virtual std::unique_ptr<TabInterface> RemoveTabAtIndexRecursive(size_t index);

```

