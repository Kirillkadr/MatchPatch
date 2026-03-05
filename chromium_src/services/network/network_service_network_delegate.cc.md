### match
```
... >>> 
 . 
 AnnotateAndMoveUserBlockedCookies 
 (  <<<
 ... ) ...
```
### patch
```
           .AnnotateAndMoveUserBlockedEphemeralCookies(

```

### match
```
...
 namespace network { ... 
 bool NetworkServiceNetworkDelegate::OnCanSetCookie(
    const net::URLRequest& request,
    const net::CanonicalCookie& cookie,
    net::CookieOptions* options,
    const net::FirstPartySetMetadata& first_party_set_metadata,
    net::CookieInclusionStatus* inclusion_status) { ...   >>> 
 network_context_->cookie_manager()->cookie_settings().IsCookieAccessible 
 (  <<< ... ) ...  } ...  } ...  
```
### patch
```
      network_context_->cookie_manager()->cookie_settings().IsEphemeralCookieAccessible(

```

### match
```
...
 namespace network { ... 
 bool NetworkServiceNetworkDelegate::OnCanSetCookie(
    const net::URLRequest& request,
    const net::CanonicalCookie& cookie,
    net::CookieOptions* options,
    const net::FirstPartySetMetadata& first_party_set_metadata,
    net::CookieInclusionStatus* inclusion_status) { ... 
return true;
 } 
 >>> 
 ... } ...  
```
### patch
```
#define IsPrivacyModeEnabled IsEphemeralPrivacyModeEnabled

```

### match
```
...
 namespace network { ... 
 int NetworkServiceNetworkDelegate::HandleClearSiteDataHeader(
    net::URLRequest* request,
    net::CompletionOnceCallback callback,
    const net::HttpResponseHeaders* original_response_headers) { ... 
return net::ERR_IO_PENDING;
 } 
 >>> 
 ... } ...  
```
### patch
```
#undef IsPrivacyModeEnabled

```

