### match
```cpp
...
 
 namespace chrome { ...   >>> 
 void 
 AddMetricsExtraParts(ChromeBrowserMainParts* main_parts) 
 {  <<< 
main_parts->AddParts(std::make_unique<ChromeBrowserMainExtraPartsMetrics>());
 ... } ...  } ...  
```
### patch
```cpp
void AddMetricsExtraParts(ChromeBrowserMainParts_ChromiumImpl* main_parts) {

```

