### match
```cpp
...
 NS_ASSUME_NONNULL_END 
 >>> 
 ... 
```
### patch
```cpp
// Expose the underlying net::X509Certificate that is not public so that
// cwv_x509_certificate_extras.mm can access the private property and expose
// additional functionality
@interface CWVX509Certificate (Internal)
@property(readonly) scoped_refptr<net::X509Certificate> internalCertificate;
@end

```

