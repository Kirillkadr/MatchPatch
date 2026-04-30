### match
```cpp
...
 NS_ASSUME_NONNULL_END 
 >>> 
 ... 
```
### patch
```cpp
// Expose the underlying web::SSLStatus that is not public so that
// cwv_ssl_status_extras.mm can access the private property and expose
// additional functionality
@interface CWVSSLStatus (Internal)
@property(readonly) web::SSLStatus internalStatus;
@end

```

