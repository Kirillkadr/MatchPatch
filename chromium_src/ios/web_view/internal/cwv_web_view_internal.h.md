### match
```cpp
...
 NS_ASSUME_NONNULL_END 
 >>> 
 ... 
```
### patch
```cpp
NS_ASSUME_NONNULL_BEGIN
namespace base {
class Value;
}

// Expose the underlying web::WebState and a few other properties that are not
// public so that cwv_web_view_extras.mm can access the private property and
// implement additional functionality
@interface CWVWebView (Internal)
@property(readonly) web::WebState* webState;
+ (BOOL)_isRestoreDataValid:(NSData*)data;
+ (id)objectFromValue:(const base::Value*)value;
@end

NS_ASSUME_NONNULL_END

```

