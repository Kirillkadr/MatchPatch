### match
```
...
 # ifndef ... 
 namespace 
 blink 
 { 
 >>> 
class CORE_EXPORT LinkLoaderClient : public GarbageCollectedMixin {
 public:
  virtual ~LinkLoaderClient() = default;
  void Trace(Visitor* visitor) const override {}

  virtual bool ShouldLoadLink() = 0;

  virtual void LinkLoaded() = 0;
  virtual void LinkLoadingErrored() = 0;
  // There is no notification for cancellation.

  virtual bool IsLinkCreatedByParser() = 0;
}
 ... } ...  
```
### patch
```
class HTMLLinkElement;

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT LinkLoaderClient : public GarbageCollectedMixin { ... 
// There is no notification for cancellation.
 virtual bool IsLinkCreatedByParser() = 0; 
 >>> 
 ... } ...  } ...  
```
### patch
```
  virtual HTMLLinkElement* GetOwner() = 0;

```

