### match
```
...
 # ifndef ... 
 namespace blink { ... 
blink::WebScopedVirtualTimePauser CreateWebScopedVirtualTimePauser(
      const char* name,
      WebScopedVirtualTimePauser::VirtualTaskDuration duration) override;
 LocalDOMWindow* GetDOMWindow() override; 
 >>> 
private
 ... } ...  
```
### patch
```
 private:
  void NotUsed();

 public:
  StorageType storage_type() const { return storage_type_; }


```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class StorageArea final : public ScriptWrappable,
                          public ExecutionContextClient,
                          public CachedStorageArea::Source { ... 
mutable bool can_access_storage_cached_result_ = false;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```
MODULES_EXPORT PageGraphObject ToPageGraphObject(StorageArea* storage_area);

```

