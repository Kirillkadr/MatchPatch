### match
```cpp
...
 #include <utility>
 
 >>> 
 ...
```
### patch
```cpp
#include "base/check_op.h"

```

### match
```cpp
...
 
 RoundedOmniboxResultsFrame::RoundedOmniboxResultsFrame(
    views::View* contents,
    LocationBar* location_bar,
    bool forward_mouse_events)
    : contents_(contents), forward_mouse_events_(forward_mouse_events) { ... 
  
>>> 
 views::ShapeContextTokens::kOmniboxExpandedRadius 
 ) 
 ; 
<<< 
...} ...
```
### patch
```cpp
views::ShapeContextTokensOverride::kOmniboxExpandedRadius);

```

### match
```cpp
...
 
 void RoundedOmniboxResultsFrame::SetElevation(int elevation) { ... 

>>> 
 views::ShapeContextTokens::kOmniboxExpandedRadius 
 ) 
 ; 
<<< 
...} ...
```
### patch
```cpp
views::ShapeContextTokensOverride::kOmniboxExpandedRadius);

```

### match
```cpp
...
 
 gfx::Insets RoundedOmniboxResultsFrame::GetContentInsets() { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp
// static
int RoundedOmniboxResultsFrame::GetShadowElevation() {
  // Expose a constant defined in cc file.
  return kElevation;
}


```

