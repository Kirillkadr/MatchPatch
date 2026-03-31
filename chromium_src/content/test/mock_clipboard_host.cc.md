### match
```cpp
...
 
 namespace content { ... 
#if BUILDFLAG(IS_MAC)
void MockClipboardHost::WriteStringToFindPboard(const std::u16string& text) {}

void MockClipboardHost::GetPlatformPermissionState(
    GetPlatformPermissionStateCallback callback) {
  std::move(callback).Run(
      blink::mojom::PlatformClipboardPermissionState::kAllow);
}
#endif
 } 
 // namespace content 
 >>> 
 ... 
```
### patch
```cpp
namespace content {

void MockClipboardHost::SanitizeOnNextWriteText() {}

}  // namespace content
```

