### match
```
...
 namespace network { ... 
 class RestrictedCookieManager::Listener : public base::LinkNode<Listener> { ... 
 void OnCookieChange(const net::CookieChangeInfo& change) { ...   >>> 
 if 
 ( 
 ! 
 restricted_cookie_manager_->cookie_settings().IsCookieAccessible 
 (  <<< ... 
change.cookie
 ... ) ...  ) ...  } ...  } ...  } ...  
```
### patch
```
    if (!restricted_cookie_manager_->cookie_settings().IsEphemeralCookieAccessible(

```

### match
```
...
 namespace network { ... 
 void RestrictedCookieManager::CookieListToGetAllForUrlCallback(
    const GURL& url,
    const net::SiteForCookies& site_for_cookies,
    const url::Origin& top_frame_origin,
    const url::Origin& isolated_top_frame_origin,
    bool is_ad_tagged,
    const net::CookieSettingOverrides& cookie_setting_overrides,
    const net::CookieOptions& net_options,
    mojom::CookieManagerGetOptionsPtr options,
    GetAllForUrlCallback callback,
    const net::CookieAccessResultList& cookie_list,
    const net::CookieAccessResultList& excluded_list) { ...   >>> 
 cookie_settings().AnnotateAndMoveUserBlockedCookies 
 (  <<< ... ) ...  } ...  } ...  
```
### patch
```
  cookie_settings().AnnotateAndMoveUserBlockedEphemeralCookies(

```

### match
```
...
>>>
 bool 
 blocked 
 = 
 ! 
 cookie_settings_->IsCookieAccessible 
 (  <<< ... ) ...  
```
### patch
```
  // IsEphemeralCookieAccessible and AnnotateAndMoveUserBlockedEphemeralCookies declared &
// defined via a chromium_src override for network/cookie_settings.{h,cc}.
  bool blocked = !cookie_settings_->IsEphemeralCookieAccessible(

```

### match
```
...
 namespace network { ... 
 void RestrictedCookieManager::CookiesEnabledFor(
    const GURL& url,
    const net::SiteForCookies& site_for_cookies,
    const url::Origin& top_frame_origin,
    net::StorageAccessApiStatus storage_access_api_status,
    bool apply_devtools_overrides,
    CookiesEnabledForCallback callback) { ...   >>> 
 std::move(callback).Run 
 ( 
 cookie_settings_->IsFullCookieAccessAllowed 
 (  <<< ... ) ...  ) ...  } ...  } ...  
```
### patch
```
  std::move(callback).Run(cookie_settings_->IsEphemeralCookieAccessAllowed(

```

### match
```
...
 namespace network { ... 
 void RestrictedCookieManager::CallCookiesAccessed() { ... 
cookie_observer_->OnCookiesAccessed(std::move(cookie_access_details_));
 } 
 >>> 
 ... } ...  
```
### patch
```
net::CookieOptions RestrictedCookieManager::MakeOptionsForSet(
    mojom::RestrictedCookieManagerRole role,
    const GURL& url,
    const net::SiteForCookies& site_for_cookies,
    const CookieSettings& cookie_settings) const {
  net::CookieOptions cookie_options = ::network::MakeOptionsForSet(
      role, url, site_for_cookies, cookie_settings);
  net::FillEphemeralStorageParams(url, site_for_cookies, BoundTopFrameOrigin(),
                                  cookie_store_->cookie_access_delegate(),
                                  &cookie_options);
  return cookie_options;
}
net::CookieOptions RestrictedCookieManager::MakeOptionsForGet(
    mojom::RestrictedCookieManagerRole role,
    const GURL& url,
    const net::SiteForCookies& site_for_cookies,
    const CookieSettings& cookie_settings) const {
  net::CookieOptions cookie_options = ::network::MakeOptionsForGet(
      role, url, site_for_cookies, cookie_settings);
  net::FillEphemeralStorageParams(url, site_for_cookies, BoundTopFrameOrigin(),
                                  cookie_store_->cookie_access_delegate(),
                                  &cookie_options);
  return cookie_options;
}

```

