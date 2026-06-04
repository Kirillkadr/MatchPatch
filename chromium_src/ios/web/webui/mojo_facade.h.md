### match
```cpp
...
 
 # ifndef ... 
#include <string>

 #include <unordered_map>
 
 >>> 
#include "base/functional/callback.h"

 ...
```
### patch
```cpp
#include <WebKit/WebKit.h>
#include "url/gurl.h"

```

### match
```cpp
...
 
 >>> 
std::string HandleMojoMessage(const std::string& mojo_message_as_json);
 ...
```
### patch
```cpp
std::string Dummy();
  bool IsWebUIMessageAllowedForFrame(const GURL& origin, NSString* prompt);

```

### match
```cpp
...
   >>> 
 void OnWatcherCallback(int callback_id, int watch_id, MojoResult result);  <<< 
 ...
```
### patch
```cpp
void OnWatcherCallback(int callback_id, int watch_id, std::string frame_id, MojoResult result);

```

