### match
```cpp
...
- (CWVSecurityStyle)securityStyle {
  return CWVSecurityStyleFromWebSecurityStyle(_internalStatus.security_style);
}

- (BOOL)hasOnlySecureContent {
  return _internalStatus.security_style == web::SECURITY_STYLE_AUTHENTICATED &&
         !(_internalStatus.content_status &
           web::SSLStatus::DISPLAYED_INSECURE_CONTENT);
}

- (CWVCertStatus)certStatus {
  return CWVCertStatusFromNetCertStatus(_internalStatus.cert_status);
}
 @ 
 end 
 >>> 
 ... 
```
### patch
```cpp
@implementation CWVSSLStatus (Internal)
- (web::SSLStatus)internalStatus {
  return _internalStatus;
}
@end
```

