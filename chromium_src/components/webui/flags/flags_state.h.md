### match
```cpp
...
 
 namespace flags_ui { ... 
 
 class FlagsState { ... 
>>> 
 void 
 GetFlagFeatureEntries 
 ( 
 FlagsStorage* flags_storage 
 , 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
  void GetFlagFeatureEntries(FlagsStorage* flags_storage,

```

### match
```cpp
...
 
 namespace flags_ui { ... 
 
 class FlagsState { ... 
 base::RepeatingCallback<bool(const FeatureEntry&)> skip_feature_entry 
 ) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  base::ListValue CreateOptionsData(
      const FeatureEntry& entry, const std::set<std::string>& enabled_entries) 
      const;

```

