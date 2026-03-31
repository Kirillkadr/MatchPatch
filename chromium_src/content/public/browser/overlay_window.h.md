### match
```cpp
...
 
 # ifndef ... 
#define CONTENT_PUBLIC_BROWSER_OVERLAY_WINDOW_H_

 #include <memory>
 
 >>> 
#include "services/media_session/public/cpp/media_image.h"

 ... 
```
### patch
```cpp
#include <optional>

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace gfx { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp
namespace media_session {
struct MediaPosition;
}  // namespace media_session

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
virtual gfx::Rect GetBounds() = 0;
 virtual void UpdateNaturalSize(const gfx::Size& natural_size) = 0; 
 >>> 
virtual void SetPlaybackState(PlaybackState playback_state) = 0;
 ... } ...  
```
### patch
```cpp
  virtual void SetMediaPosition(                                                         
      const std::optional<media_session::MediaPosition>& media_position) {}
  virtual void SetSeekerEnabled(bool enabled) {}

```

