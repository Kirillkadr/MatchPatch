### match
```cpp
...
 
 # ifndef ... 
// embedder delegate, which cancels all async operations managed by them.
 void Cancel() override; 
 >>> 
bool IsPermissionRequestSupported(
      permissions::RequestType request_type) override;
 ... 
```
### patch
```cpp
  bool IsPermissionRequestSupported_ChromiumImpl(
      permissions::RequestType request_type);

```

