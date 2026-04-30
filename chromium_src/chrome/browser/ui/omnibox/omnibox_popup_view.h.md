### match
```cpp
...
 class OmniboxSuggestionButtonRowView 
 ; 
 >>> 
namespace ui {
struct AXNodeData;
}
 ... 
```
### patch
```cpp
class BraveOmniboxResultView;


```

### match
```cpp
...
virtual bool IsSelectionPopupControlled() const = 0;
 protected 
 : 
 >>> 
friend class OmniboxResultView;
 ... 
```
### patch
```cpp
  friend class BraveOmniboxResultView;

```

