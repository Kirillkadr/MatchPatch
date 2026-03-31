### match
```cpp
...
 const base::FeatureParam<std::string> kAggregationServiceCoordinatorAllowlist{
    &kAggregationServiceMultipleCloudProviders, "allowlist", ""};
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kAggregationServiceMultipleCloudProviders,
     base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

