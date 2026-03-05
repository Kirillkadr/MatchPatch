### match
```
...
#include "url/origin.h"

 #include "url/url_constants.h"
 
 >>> 
#if BUILDFLAG(IS_ANDROID)
#include "net/android/network_library.h"
#endif
 ... 
```
### patch
```
#include "net/http/transport_security_state.h"

```

### match
```
...
 if (TransportSecurityState* hsts =
          request->context()->transport_security_state()) { ...   >>> 
 upgrade_decision 
 = 
 hsts->GetSSLUpgradeDecision 
 ( 
 url.GetHost() 
 , 
 /*is_top_level_nav=*/ 
 request->isolation_info().IsOutermostMainFrameRequest() 
 ,  <<< ... 
request->net_log()
 ... ) ...  } ...  
```
### patch
```
    upgrade_decision = hsts->GetSSLUpgradeDecision(request->isolation_info().network_anonymization_key(),url.GetHost(),/*is_top_level_nav=*/request->isolation_info().IsOutermostMainFrameRequest(),

```

### match
```
...
 namespace net { ... 
 void URLRequestHttpJob::ProcessStrictTransportSecurityHeader() { ... 
 if ((value =
           headers->EnumerateHeader(nullptr, "Strict-Transport-Security"))) { ...   >>> 
 security_state->AddHSTSHeader(request_info_.url.GetHost(), *value);  <<< ... } ...  } ...  } ...  
```
### patch
```
    security_state->AddHSTSHeader(request_->isolation_info(), request_info_.url.GetHost(), *value);

```

### match
```
...
 namespace net { ... 
 void URLRequestHttpJob::OnStartCompleted(int result) { ... 
 if (IsCertificateError(result)) { ... 
 NotifySSLCertificateError ( ...   >>> 
 state->ShouldSSLErrorsBeFatal(request_info_.url.GetHost()) 
 &&  <<< ... 
result != ERR_CERT_KNOWN_INTERCEPTION_BLOCKED
 ... ) ...  } ...  } ...  } ...  
```
### patch
```
        state->ShouldSSLErrorsBeFatal(request_->isolation_info().network_anonymization_key(), request_info_.url.GetHost()) &&

```

### match
```
...
 namespace net { ... 
 bool URLRequestHttpJob::ShouldRecordPartitionedCookieUsage() const { ... 
return request_->cookie_partition_key().has_value();
 } 
 >>> 
 ... } ...  
```
### patch
```
namespace {
// This function acts as a trampoline between
// `URLRequestHttpJob::CreateCookieOptions` and the `CreateCookieOptions`
// declared in the annonymous namespace inside `net::`. This is necessary
// because otherwise there's no way for `URLRequestHttpJob::CreateCookieOptions`
// to capture calls to `CreateCookieOptions` and at the same time be able to
// call it in the annonymous namespace.
CookieOptions CreateCookieOptionsCaller(
    CookieOptions::SameSiteCookieContext same_site_context) {
  return CreateCookieOptions(same_site_context);
}

}  // namespace

CookieOptions URLRequestHttpJob::CreateCookieOptions(
    CookieOptions::SameSiteCookieContext same_site_context) const {
  CookieOptions cookie_options = CreateCookieOptionsCaller(same_site_context);
  FillEphemeralStorageParams(
      request_->url(), request_->site_for_cookies(),
      request_->isolation_info().top_frame_origin(),
      request_->context()->cookie_store()->cookie_access_delegate(),
      &cookie_options);
  return cookie_options;
}

```

