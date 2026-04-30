### match
```cpp
...
 
 # ifndef ... 
 class PageInfoUI 
 ; 
 >>> 
// The |PageInfo| provides information about a website's permissions,
 ... 
```
### patch
```cpp
#define PageInfo PageInfo_ChromiumImpl

```

### match
```cpp
...
 
 # ifndef ... 
 
 class PageInfo : private content_settings::CookieControlsObserver,
                 public content_settings::PageSpecificContentSettings::
                     PermissionUsageObserver { ...   >>> 
 std::set<net::SchemefulSite> 
 GetTwoSitePermissionRequesters 
 (  <<< 
ContentSettingsType type
 ... ) ...  } ...  
```
### patch
```cpp
  protected:
  virtual std::set<net::SchemefulSite> GetTwoSitePermissionRequesters(

```

### match
```cpp
...
 
 # ifndef ... 
 
 class PageInfo : private content_settings::CookieControlsObserver,
                 public content_settings::PageSpecificContentSettings::
                     PermissionUsageObserver { ... 
base::WeakPtrFactory<PageInfo> weak_factory_{this};
 } 
 ; 
 >>> 
 ... 
```
### patch
```cpp
#undef PageInfo
class PageInfo : public PageInfo_ChromiumImpl {
 public:
  using PageInfo_ChromiumImpl::PageInfo_ChromiumImpl;
  PageInfo(const PageInfo&) = delete;
  PageInfo& operator=(const PageInfo&) = delete;

  ~PageInfo() override = default;

 private:
  std::set<net::SchemefulSite> GetTwoSitePermissionRequesters(
      ContentSettingsType type) override;
};

```

