### match
```cpp
...
 
 # ifndef ... 
 namespace 
 storage 
 { 
 >>> 
class BlobUrlRegistry
 ... } ...  
```
### patch
```cpp
class BlobURLStoreImpl;
using BlobURLStoreImpl_BraveImpl = BlobURLStoreImpl;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace storage { ...   >>> 
 class COMPONENT_EXPORT(STORAGE_BROWSER) 
 BlobURLStoreImpl  <<<  ...} ...  
```
### patch
```cpp
class COMPONENT_EXPORT(STORAGE_BROWSER) BlobURLStoreImpl_ChromiumImpl

```

### match
```cpp
...
// `partitioning_blob_url_closure` runs when the storage_key check fails  >>> 
 // in `BlobURLStoreImpl::ResolveAsURLLoaderFactory`. 
 BlobURLStoreImpl 
 (  <<< 
const
 ... ) ...  
```
### patch
```cpp
  // in `BlobURLStoreImpl_ChromiumImpl::ResolveAsURLLoaderFactory`.
  BlobURLStoreImpl_ChromiumImpl(

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace storage { ... 
BlobURLStoreImpl_ChromiumImpl
	: public blink::mojom::BlobURLStore {
 public:
  // `partitioning_blob_url_closure` runs when the storage_key check fails
    // in `BlobURLStoreImpl_ChromiumImpl::ResolveAsURLLoaderFactory`.
		  BlobURLStoreImpl_ChromiumImpl(
		const blink::StorageKey& storage_key,
      const url::Origin& renderer_origin,
      int render_process_host_id,
      base::WeakPtr<BlobUrlRegistry> registry,
      BlobURLValidityCheckBehavior validity_check_options =
          BlobURLValidityCheckBehavior::DEFAULT,
      base::RepeatingCallback<
          void(const GURL&,
               std::optional<blink::mojom::PartitioningBlobURLInfo>)>
          partitioning_blob_url_closure = base::DoNothing(),
      base::RepeatingCallback<bool()> storage_access_check_closure =
          base::BindRepeating([]() -> bool { return false; }),
      std::optional<GURL> top_level_blob_document_url = std::nullopt,
      bool partitioning_disabled_by_policy = false,
      const char* context_type_for_debugging = "",
      base::RepeatingCallback<std::string()> storage_key_debug_string_callback =
          base::BindRepeating([]() -> std::string { return ""; }));  >>> 
 BlobURLStoreImpl(const BlobURLStoreImpl&) = delete; 
 BlobURLStoreImpl& operator=(const BlobURLStoreImpl&) = delete;  <<< 
~BlobURLStoreImpl() override
 ... } ...  } ...  
```
### patch
```cpp
  BlobURLStoreImpl_ChromiumImpl(const BlobURLStoreImpl_ChromiumImpl&) = delete;
  BlobURLStoreImpl_ChromiumImpl& operator=(const BlobURLStoreImpl_ChromiumImpl&) = delete;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace storage { ... 
BlobURLStoreImpl_ChromiumImpl& operator=(const BlobURLStoreImpl_ChromiumImpl&) = delete;  >>> 
 ~BlobURLStoreImpl() override 
 ;  <<< 
void Register(
      mojo::PendingRemote<blink::mojom::Blob> blob,
      const GURL& url,
      RegisterCallback callback) override;
 ... } ...  
```
### patch
```cpp

  ~BlobURLStoreImpl_ChromiumImpl() override;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace storage { ... 
// this function is only suitable to be called from `Register()` and
 // `Revoke()`. 
 >>> 
bool BlobUrlIsValid(const GURL& url, const char* method) const;
 ... } ...  
```
### patch
```cpp
  friend BlobURLStoreImpl_BraveImpl;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace storage { ... 
base::RepeatingCallback<bool()> storage_access_check_callback_;  >>> 
 // Set when this BlobURLStoreImpl corresponds to a top-level document created  <<< 
// by navigating to a blob URL.
 ... } ...  
```
### patch
```cpp
  // Set when this BlobURLStoreImpl_ChromiumImpl corresponds to a top-level document created

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace storage { ... 
base::RepeatingCallback<std::string()> storage_key_debug_string_callback_;  >>> 
 base::WeakPtrFactory<BlobURLStoreImpl> weak_ptr_factory_{this};  <<<  ...} ...  
```
### patch
```cpp
  base::WeakPtrFactory<BlobURLStoreImpl_ChromiumImpl> weak_ptr_factory_{this};

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace storage { ... 
base::WeakPtrFactory<BlobURLStoreImpl_ChromiumImpl> weak_ptr_factory_{this};
 } 
 ; 
 >>> 
}
 ... 
```
### patch
```cpp
class COMPONENT_EXPORT(STORAGE_BROWSER) BlobURLStoreImpl
    : public BlobURLStoreImpl_ChromiumImpl {
 public:
  using BlobURLStoreImpl_ChromiumImpl::BlobURLStoreImpl_ChromiumImpl;
  void ResolveAsURLLoaderFactory(
      const GURL& url,
      mojo::PendingReceiver<network::mojom::URLLoaderFactory> receiver)
      override;
  void ResolveAsBlobURLToken(
      const GURL& url,
      mojo::PendingReceiver<blink::mojom::BlobURLToken> token,
      bool is_top_level_navigation) override;

 private:
  bool IsBlobResolvable(const GURL& url) const;
};

```

