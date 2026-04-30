### match
```cpp
...
#include "third_party/jni_zero/jni_zero.h"

 #endif 
 >>> 
 ...
```
### patch
```cpp
class SkBitmap;

```

### match
```cpp
...
 >>> 
virtual void CopyImageAt(int x, int y) = 0;
 ...
```
### patch
```cpp
  virtual void GetImageAt(int x, int y,                                            
             base::OnceCallback<void(const SkBitmap&)> callback) = 0;

```

