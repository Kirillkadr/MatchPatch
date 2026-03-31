### match
```cpp
...
 
 # ifndef ... 
 
 namespace screen_ai { ... 
 
 class ScreenAIInstallState { ... 
// Returns true if the library is used recently and we need to keep it on
 // device and updated. 
 >>> 
static bool ShouldInstall(PrefService* local_state);
 ... } ...  } ...  
```
### patch
```cpp
  static bool ShouldInstall_ChromiumImpl(PrefService* local_state);

```

