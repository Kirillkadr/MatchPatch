### match
```cpp
...
 
 namespace compose::features { ... 
BASE_FEATURE(kComposeAllowOnDeviceExecution, base::FEATURE_DISABLED_BY_DEFAULT);
 BASE_FEATURE(kComposeUpfrontInputModes, base::FEATURE_ENABLED_BY_DEFAULT); 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kEnableCompose, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

