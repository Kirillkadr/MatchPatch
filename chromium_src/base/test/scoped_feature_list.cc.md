### match
```
...
 namespace base::test { ... 
 void ScopedFeatureList::InitWithMergedFeatures(
    Features&& merged_features,
    bool create_associated_field_trials,
    bool keep_existing_states) { ... 
InitWithFeatureList(std::move(new_feature_list));
 } 
 >>> 
 ... } ...  
```
### patch
```
void ScopedFeatureList::InitWithFeaturesAndDisable(
    const FeatureRef& feature_to_disable,
    const std::vector<FeatureRef>& enabled_features,
    const std::vector<FeatureRef>& disabled_features) {
  std::vector all_disabled_features = disabled_features;
  all_disabled_features.push_back(feature_to_disable);
  InitWithFeatures(enabled_features, all_disabled_features);
}

```

