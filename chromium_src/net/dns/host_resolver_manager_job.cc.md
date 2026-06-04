### match
```cpp
...
 
 namespace net { ... 
 
 void HostResolverManager::Job::CompleteRequests(
    const HostCache::Entry& results,
    base::TimeDelta ttl,
    bool allow_cache,
    bool secure,
    std::optional<TaskType> task_type,
    std::optional<base::TimeDelta> task_completion_delay,
    std::optional<DohResolutionDetails> doh_details) { ... 
if (allow_cache) {
    MaybeCacheResult(results, ttl, secure);
  }
 RecordJobHistograms(results, task_type); 
 >>> 
if (results.error() == OK && had_non_speculative_request_ &&
      key_.source == HostResolverSource::ANY) {
    RecordJobHttpsHistograms();
  }
 ... } ...  } ...  
```
### patch
```cpp
  if (task_type.has_value()) {                                  
    SecureDnsCounter::GetInstance()->RecordAutoSecureTaskCount(
        static_cast<int>(*task_type), key_.query_types);
  }

```

