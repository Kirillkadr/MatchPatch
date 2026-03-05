### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT BaseFetchContext : public FetchContext { ... 
protected:
  BaseFetchContext(const DetachableResourceFetcherProperties& properties,
                   DetachableConsoleLogger* logger)
      : fetcher_properties_(properties), console_logger_(logger) {}

  // Used for security checks.  >>> 
 virtual bool AllowScript() const = 0;  <<< ... 
// Note: subclasses are expected to override following methods.
 ... } ...  } ...  
```
### patch
```
  virtual bool AllowScript(const KURL& url) const = 0;

```

