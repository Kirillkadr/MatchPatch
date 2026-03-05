### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT SchemefulSite { ... 
// in this case, and unfriend IsolationInfo.
 friend class IsolationInfo; 
 >>> 
// Needed to create a bogus origin from a site.
 ... } ...  } ...  
```
### patch
```
  friend class HSTSPartitionHashHelper;

```

