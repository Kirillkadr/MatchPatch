### match
```cpp
...
 
 namespace extension_urls { ...   >>> 
 bool 
 IsWebstoreUpdateUrl(const GURL& update_url) 
 {  <<< 
GURL store_url = GetWebstoreUpdateUrl();
 ... } ...  } ...  
```
### patch
```cpp
bool IsWebstoreUpdateUrl_ChromiumImpl(const GURL& update_url) {

```

### match
```cpp
...
 
 namespace extension_urls { ... 
 
 bool IsSafeBrowsingUrl(const GURL& url) { ... 
return origin.DomainIs("sb-ssl.google.com") ||
         origin.DomainIs("safebrowsing.googleapis.com") ||
         (origin.DomainIs("safebrowsing.google.com") &&
          base::StartsWith(path, "/safebrowsing",
                           base::CompareCase::SENSITIVE)) ||
         (safe_browsing::hash_realtime_utils::
              IsHashRealTimeLookupEligibleInSession() &&
          url == safe_browsing::kHashPrefixRealTimeLookupsRelayUrl.Get());
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
namespace {
bool IsDefaultWebstoreUpdateUrl(const GURL& update_url) {
  GURL store_url = GetDefaultWebstoreUpdateUrl();
  return (update_url.host() == store_url.host() &&
          update_url.path() == store_url.path());
}

}  // namespace

bool IsWebstoreUpdateUrl(const GURL& update_url) {
  return IsDefaultWebstoreUpdateUrl(update_url) ||
         IsWebstoreUpdateUrl_ChromiumImpl(update_url);
}

```

