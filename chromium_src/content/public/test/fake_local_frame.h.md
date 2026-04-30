### match
```cpp
...
 
 # ifndef ... 
#define CONTENT_PUBLIC_TEST_FAKE_LOCAL_FRAME_H_

 #include <optional>
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "third_party/blink/public/mojom/frame/frame.mojom.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 class FakeLocalFrame : public blink::mojom::LocalFrame { ... 
 const ::network::URLLoaderCompletionStatus& completion_status 
 ) 
 override 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  void GetImageAt(const ::gfx::Point& window_point, GetImageAtCallback callback) 
      override;

```

