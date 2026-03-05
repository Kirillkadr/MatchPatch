### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class PLATFORM_EXPORT FetchContext : public GarbageCollected<FetchContext> { ... 
virtual ~FetchContext() = default;
 virtual void Trace(Visitor*) const {} 
 >>> 
virtual void AddAdditionalRequestHeaders(ResourceRequest&);
 ... } ...  } ...  
```
### patch
```
  virtual String GetCacheIdentifierIfCrossSiteSubframe() const;

```

