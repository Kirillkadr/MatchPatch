### match
```cpp
...
 
 # ifndef ... 
#include <memory>
  >>> 
 #include "base/functional/callback.h"
  <<< 
#include "base/memory/raw_ptr.h"

 ... 
```
### patch
```cpp

```

### match
```cpp
...
 
 # ifndef ...   >>> 
 class 
 BrowserWindowFeatures_ChromiumImpl 
 {  <<< 
public
 ... } ...  
```
### patch
```cpp
class BrowserWindowFeatures {

```

### match
```cpp
...
 
 # ifndef ... 
 
 class BrowserWindowFeatures { ...   >>> 
 BrowserWindowFeatures_ChromiumImpl(); 
 ~BrowserWindowFeatures_ChromiumImpl();  <<< 
BrowserWindowFeatures_ChromiumImpl(const BrowserWindowFeatures_ChromiumImpl&) = delete;
 ... } ...  
```
### patch
```cpp
  BrowserWindowFeatures();
  ~BrowserWindowFeatures();

```

### match
```cpp
...
 
 # ifndef ... 
 
 class BrowserWindowFeatures { ... 
~BrowserWindowFeatures();  >>> 
 BrowserWindowFeatures_ChromiumImpl(const BrowserWindowFeatures_ChromiumImpl&) = delete; 
 BrowserWindowFeatures_ChromiumImpl& operator=(const BrowserWindowFeatures_ChromiumImpl&) = delete;  <<< 
// Called exactly once to initialize features. This is called prior to
 ... } ...  
```
### patch
```cpp

  BrowserWindowFeatures(const BrowserWindowFeatures&) = delete;
  BrowserWindowFeatures& operator=(const BrowserWindowFeatures&) = delete;

```

### match
```cpp
...
 
 # ifndef ... 
// in this class.  >>> 
 virtual void Init(BrowserWindowInterface* browser);  <<< 
// Called exactly once to initialize features that depend on the window object
 ... 
```
### patch
```cpp
  void Init(BrowserWindowInterface* browser);

```

### match
```cpp
...
 
 # ifndef ... 
// being created.  >>> 
 virtual void InitPostWindowConstruction(Browser* browser);  <<< 
// Called exactly once to initialize features that depend on the view
 ... 
```
### patch
```cpp
  void InitPostWindowConstruction(Browser* browser);

```

### match
```cpp
...
 
 # ifndef ... 
// hierarchy in BrowserView.  >>> 
 virtual void InitPostBrowserViewConstruction(BrowserView* browser_view);  <<< 
// Called exactly once to tear down state that depends on the window object.
 ... 
```
### patch
```cpp
  void InitPostBrowserViewConstruction(BrowserView* browser_view);

```

### match
```cpp
...
 
 # ifndef ... 
// Called exactly once to tear down state that depends on the window object.  >>> 
 virtual void TearDownPreBrowserWindowDestruction(); 
 friend BraveBrowserWindowFeatures;  <<< 
BrowserActions* browser_actions() { return browser_actions_.get(); }
 ... 
```
### patch
```cpp
  void TearDownPreBrowserWindowDestruction();


```

### match
```cpp
...
 
 # ifndef ... 
 
 class BrowserWindowFeatures { ... 
ExclusiveAccessManager*  exclusive_access_manager() {
    return exclusive_access_manager_.get();
  }  >>> 
 const ExclusiveAccessManager* exclusive_access_manager() const {
    return exclusive_access_manager_.get();
  }  <<< 
FullscreenControlHost* fullscreen_control_host() {
    return fullscreen_control_host_.get();
  }
 ... } ...  
```
### patch
```cpp

```

