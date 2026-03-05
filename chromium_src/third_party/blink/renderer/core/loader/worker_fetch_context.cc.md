### match
```
...
 namespace blink { ...   >>> 
 bool 
 WorkerFetchContext::AllowScript() const 
 {  <<< ... 
// Script is always allowed in worker fetch contexts, since the fact that
 ... } ...  } ...  
```
### patch
```
bool WorkerFetchContext::AllowScript_Unused() const {

```

### match
```
...
 namespace blink { ... 
 void WorkerFetchContext::Trace(Visitor* visitor) const { ... 
BaseFetchContext::Trace(visitor);
 } 
 >>> 
 ... } ...  
```
### patch
```
bool WorkerFetchContext::AllowScript(const KURL& url) const {
  if (!global_scope_->ContentSettingsClient()) {
    return true;
  }
  // If we're on a worker, script should be enabled, so no need to plumb
  // Settings::GetScriptEnabled() here.
  return global_scope_->ContentSettingsClient()->AllowScriptFromSource(true,
                                                                       url);
}

```

