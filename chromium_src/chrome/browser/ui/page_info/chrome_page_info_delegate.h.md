### match
```cpp
...
bool HasAutoPictureInPictureBeenRegistered() override;  >>> 
 bool IsContentDisplayedInVrHeadset() override;  <<< 
security_state::SecurityLevel GetSecurityLevel() override;
 ... 
```
### patch
```cpp
  bool  BraveShouldShowPermission(ContentSettingsType type) override; 
  virtual bool IsContentDisplayedInVrHeadset() override;

```

