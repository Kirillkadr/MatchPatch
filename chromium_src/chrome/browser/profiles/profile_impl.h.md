### match
```cpp
...
 
 # ifndef ... 
bool WasCreatedByVersionOrLater(const std::string& version) override;  >>> 
 bool ShouldRestoreOldSessionCookies() override;  <<< 
bool ShouldPersistSessionCookies() const override;
 ... 
```
### patch
```cpp
  bool ShouldRestoreOldSessionCookies_ChromiumImpl();
  bool ShouldRestoreOldSessionCookies() override;

```

