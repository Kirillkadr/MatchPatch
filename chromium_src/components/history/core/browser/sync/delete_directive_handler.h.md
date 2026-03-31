### match
```cpp
...
 
 # ifndef ... 
 
 namespace history { ... 
 
 class DeleteDirectiveHandler final : public syncer::SyncableService { ... 
// Create delete directives for the deletion of visits in the time range
 // specified by `begin_time` and `end_time`. 
 >>> 
bool CreateTimeRangeDeleteDirective(base::Time begin_time,
                                      base::Time end_time);
 ... } ...  } ...  
```
### patch
```cpp
  bool CreateUrlDeleteDirective_ChromiumImpl(const GURL& url); \

```

