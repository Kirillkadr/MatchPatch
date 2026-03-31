### match
```cpp
...
>>>
 proto::OptimizationTarget 
 GetOptimizationTargetForFeature 
 (  <<< 
mojom::OnDeviceFeature feature
 ... ) ...  
```
### patch
```cpp
proto::OptimizationTarget GetOptimizationTargetForFeature_ChromiumImpl(

```

### match
```cpp
...
 
 namespace optimization_guide { ... 
 
 std::optional<mojom::OnDeviceFeature> GetFeatureForUseCase(
    const std::string& use_case_name) { ... 
return it->second;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
COMPONENT_EXPORT(OPTIMIZATION_GUIDE_FEATURES)
proto::OptimizationTarget GetOptimizationTargetForFeature(
    mojom::OnDeviceFeature feature) {
  return proto::OPTIMIZATION_TARGET_UNKNOWN;
}

```

