### match
```cpp

...
 # ifndef ... 
#include "ui/views/style/typography.h"

 #include "ui/views/view.h"
 
 >>> 
namespace views {
...
}
 ... } ...  
```
### patch
```cpp

class CustomStyledLabel;

```

### match
```cpp

...
>>>
 std::unique_ptr<Label> 
 CreateLabel 
 (  <<< ... 
const std::u16string& text
 ... ) ...  
```
### patch
```cpp


  friend class ::CustomStyledLabel;                                        \
  virtual std::unique_ptr<views::Label> CreateLabel(

```

