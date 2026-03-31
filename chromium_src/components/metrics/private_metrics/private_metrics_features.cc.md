### match
```cpp
...
 
 namespace metrics::private_metrics { ... 
// 1 MiB
 BASE_FEATURE(kPrivateMetricsPumaRc, base::FEATURE_DISABLED_BY_DEFAULT); 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kPrivateMetricsFeature, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

