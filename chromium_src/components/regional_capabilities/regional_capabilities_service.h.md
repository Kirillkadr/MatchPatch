### match
```cpp
...
 
 namespace regional_capabilities { ... 
 
 class RegionalCapabilitiesService : public KeyedService { ... 
std::vector<const TemplateURLPrepopulateData::PrepopulatedEngine*>
 GetRegionalPrepopulatedEngines() 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  TemplateURLPrepopulateData::BravePrepopulatedEngineID GetRegionalDefaultEngine();

```

