### match
```cpp
...
 
 # ifndef ... 
 
 namespace gcm { ... 
 
 class GCMDriver { ... 
// Get GCM client internal states and statistics. The activity logs will be
 // cleared before returning the stats when |clear_logs| is set to CLEAR_LOGS. 
 >>> 
virtual void GetGCMStatistics(GetGCMStatisticsCallback callback,
                                ClearActivityLogs clear_logs) = 0;
 ... } ...  } ...  
```
### patch
```cpp
  virtual void SetEnabled(bool enabled) {} 

```

