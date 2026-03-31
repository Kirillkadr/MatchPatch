### match
```cpp
...
 
 # ifndef ... 
 NS_ASSUME_NONNULL_BEGIN 
 >>> 
 ... 
```
### patch
```cpp
// This override just exposes the internally held web::DownloadTask as a
// property so that we can add additional methods to CWVDownloadTask that use
// it such as exposing the originating host
namespace web {
class DownloadTask;
}

```

### match
```cpp
...
 NS_ASSUME_NONNULL_END 
 >>> 
 ... 
```
### patch
```cpp
@interface CWVDownloadTask (Internal)
@property(readonly) web::DownloadTask* internalTask;
@end

```

