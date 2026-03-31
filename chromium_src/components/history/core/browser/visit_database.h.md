### match
```cpp
...
 
 # ifndef ... 
 
 namespace history { ... 
 
 class VisitDatabase { ... 
// timestamps are converted to dates using local time. Returns false if there
 // is a failure executing the statement. True otherwise. 
 >>> 
bool GetHistoryCount(const base::Time& begin_time,
                       const base::Time& end_time,
                       VisitQuery404sPolicy policy_for_404_visits,
                       int* count);
 ... } ...  } ...  
```
### patch
```cpp
  bool GetKnownToSyncCount(int* count); 

```

