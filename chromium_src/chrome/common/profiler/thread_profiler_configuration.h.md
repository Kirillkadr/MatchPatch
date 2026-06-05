### match
```cpp
...
 
 class ThreadProfilerConfiguration { ... 
bool IsProfilerEnabledForCurrentProcess() const;
 // True if the profiler should be started for |thread| in the current process. 
 >>> 
bool IsProfilerEnabledForCurrentProcessAndThread(
      sampling_profiler::ProfilerThreadType thread) const;
 ... } ...  
```
### patch
```cpp
  bool IsProfilerEnabledForCurrentProcessAndThread_ChromiumImpl(
      sampling_profiler::ProfilerThreadType thread) const;

```

