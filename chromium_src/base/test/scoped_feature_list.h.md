### match
```
...
 # ifndef ... 
 namespace base::test { ... 
// interactions.  >>> 
 void InitWithFeatures(const std::vector<FeatureRef>& enabled_features,
                        const std::vector<FeatureRef>& disabled_features);  <<< ... 
// Initializes and registers a FeatureList instance based on the current
 ... } ...  
```
### patch
```
  void  InitWithFeaturesAndDisable(const FeatureRef& feature_to_disable, const std::vector<FeatureRef>& enabled_features,
                        const std::vector<FeatureRef>& disabled_features);
  void InitWithFeatures(const std::vector<FeatureRef>& enabled_features,
                        const std::vector<FeatureRef>& disabled_features)

```

