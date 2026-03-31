### match
```cpp
...
>>>
 void 
 ProfileMetrics::LogProfileAvatarSelection(size_t icon_index) 
 {  <<< 
ProfileAvatar icon_name = AVATAR_UNKNOWN;
 ... } ...  
```
### patch
```cpp
void ProfileMetrics::LogProfileAvatarSelection_ChromiumImpl(size_t icon_index) {

```

### match
```cpp
...
 
 void ProfileMetrics::LogProfileLaunch(Profile* profile) { ... 
if (profile->IsChild()) {
    base::RecordAction(
        base::UserMetricsAction("ManagedMode_NewManagedUserWindow"));
  }
 } 
 >>> 
 ... 
```
### patch
```cpp
void ProfileMetrics::LogProfileAvatarSelection(size_t icon_index) { }
```

