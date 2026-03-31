### match
```cpp
...
 
 namespace metrics::structured { ... 
 
 double GetMaxDiskSizeRatio() { ... 
return kMaxDiskSizeQuota.Get();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kPhoneHubStructuredMetrics, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

