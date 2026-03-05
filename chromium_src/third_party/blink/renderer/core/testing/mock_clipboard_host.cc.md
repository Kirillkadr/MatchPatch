### match
```
...
 namespace blink { ... 
void MockClipboardHost::GetPlatformPermissionState(
    GetPlatformPermissionStateCallback callback) {
  std::move(callback).Run(platform_permission_state_);
}
 #endif 
 >>> 
 ... } ...  
```
### patch
```
void MockClipboardHost::SanitizeOnNextWriteText() {}

```

