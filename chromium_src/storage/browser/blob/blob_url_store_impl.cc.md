### match
```cpp

...
#include "storage/browser/blob/blob_url_store_impl.h"

 #include <algorithm>
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```cpp

#include "storage/browser/blob/blob_url_store_impl.h"
#include "storage/browser/blob/blob_url_utils.h"

```

### match
```cpp

...
 namespace storage { ...   >>> 
 BlobURLStoreImpl::BlobURLStoreImpl 
 (  <<< ... 
const blink::StorageKey& storage_key
 ... ) ...  } ...  
```
### patch
```cpp

BlobURLStoreImpl_ChromiumImpl::BlobURLStoreImpl_ChromiumImpl(

```

### match
```cpp

...
 namespace storage { ...   >>> 
 BlobURLStoreImpl::~BlobURLStoreImpl() 
 {  <<< ... 
if (registry_) {
    for (const auto& url : urls_)
      registry_->RemoveUrlMapping(url, storage_key_);
  }
 ... } ...  } ...  
```
### patch
```cpp

BlobURLStoreImpl_ChromiumImpl::~BlobURLStoreImpl_ChromiumImpl() {

```

### match
```cpp

...
 namespace storage { ...   >>> 
 void 
 BlobURLStoreImpl::Register 
 (  <<< ... 
mojo::PendingRemote<blink::mojom::Blob> blob
 ... ) ...  } ...  
```
### patch
```cpp

void BlobURLStoreImpl_ChromiumImpl::Register(

```

### match
```cpp

...
 namespace storage { ...   >>> 
 void 
 BlobURLStoreImpl::Revoke(const GURL& url) 
 {  <<< ... 
if (!BlobUrlIsValid(url, "Revoke"))
    return;
 ... } ...  } ...  
```
### patch
```cpp

void BlobURLStoreImpl_ChromiumImpl::Revoke(const GURL& url) {

```

### match
```cpp

...
 namespace storage { ...   >>> 
 bool 
 BlobURLStoreImpl::ShouldPartitionBlobUrlAccess 
 (  <<< ... 
bool has_storage_access_handle
 ... ) ...  } ...  
```
### patch
```cpp

bool BlobURLStoreImpl_ChromiumImpl::ShouldPartitionBlobUrlAccess(

```

### match
```cpp

...
 namespace storage { ...   >>> 
 void 
 BlobURLStoreImpl::ResolveAsURLLoaderFactory 
 (  <<< ... 
const GURL& url
 ... ) ...  } ...  
```
### patch
```cpp

void BlobURLStoreImpl_ChromiumImpl::ResolveAsURLLoaderFactory(

```

### match
```cpp

...
 namespace storage { ...   >>> 
 void 
 BlobURLStoreImpl::ResolveAsBlobURLToken 
 (  <<< ... 
const GURL& url
 ... ) ...  } ...  
```
### patch
```cpp

void BlobURLStoreImpl_ChromiumImpl::ResolveAsBlobURLToken(

```

### match
```cpp

...
 namespace storage { ...   >>> 
 bool 
 BlobURLStoreImpl::BlobUrlIsValid 
 ( 
 const GURL& url 
 ,  <<< ... 
const char* method
 ... ) ...  } ...  
```
### patch
```cpp

bool BlobURLStoreImpl_ChromiumImpl::BlobUrlIsValid(const GURL& url,

```

### match
```cpp

...
 namespace storage { ... 
 bool BlobURLStoreImpl_ChromiumImpl::BlobUrlIsValid(const GURL& url,
	const char* method) const { ... 
return true;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp

void BlobURLStoreImpl::ResolveAsURLLoaderFactory(
    const GURL& url,
    mojo::PendingReceiver<network::mojom::URLLoaderFactory> receiver) {
  if (!IsBlobResolvable(url)) {
    BlobURLLoaderFactory::Create(mojo::NullRemote(), url, std::move(receiver));
    return;
  }

  BlobURLStoreImpl_ChromiumImpl::ResolveAsURLLoaderFactory(url,
                                                           std::move(receiver));
}

void BlobURLStoreImpl::ResolveAsBlobURLToken(
    const GURL& url,
    mojo::PendingReceiver<blink::mojom::BlobURLToken> token,
    bool is_top_level_navigation) {
  if (!IsBlobResolvable(url)) {
    return;
  }

  BlobURLStoreImpl_ChromiumImpl::ResolveAsBlobURLToken(url, std::move(token),
                                                       is_top_level_navigation);
}

bool BlobURLStoreImpl::IsBlobResolvable(const GURL& url) const {
  // Check if the URL is mapped to a BlobURLStore with the current
  // `storage_key_` or if it's an extension-generated blob.
  const GURL& clean_url = BlobUrlUtils::UrlHasFragment(url)
                              ? BlobUrlUtils::ClearUrlFragment(url)
                              : url;
  constexpr std::string_view kChromeExtensionScheme = "chrome-extension";
  return (registry_ && registry_->IsUrlMapped(clean_url, storage_key_) ==
                           BlobUrlRegistry::MappingStatus::kIsMapped) ||
         (url.SchemeIsBlob() &&
          (url::Origin::Create(url).scheme() == kChromeExtensionScheme ||
           storage_key_.origin().scheme() == kChromeExtensionScheme));
}

```

