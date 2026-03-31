### match
```cpp
...
 
 namespace screen_ai { ...   >>> 
 bool 
 ScreenAIInstallState::ShouldInstall(PrefService* local_state) 
 {  <<< 
bool device_compatible = IsDeviceCompatible();
 ... } ...  } ...  
```
### patch
```cpp
bool ScreenAIInstallState::ShouldInstall_ChromiumImpl(PrefService* local_state) {

```

### match
```cpp
...
 
 namespace screen_ai { ... 
 
 void ScreenAIInstallState::SetStateForTesting(State state) { ... 
for (ScreenAIInstallState::Observer& observer : observers_) {
    observer.StateChanged(state_);
  }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool ScreenAIInstallState::ShouldInstall(PrefService* local_state) {
  return false;
}

```

