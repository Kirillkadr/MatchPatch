### match
```cpp
...
 
 namespace content { ... 
WebContents* WebContentsDelegate::GetResponsibleWebContents(
    WebContents* web_contents) {
  return nullptr;
}
 } 
 // namespace content 
 >>> 
 ... 
```
### patch
```cpp
namespace content {
WebContents* WebContentsDelegate::AddNewContents_ChromiumImpl(
    WebContents* source,
    std::unique_ptr<WebContents> new_contents,
    const GURL& target_url,
    WindowOpenDisposition disposition,
    const blink::mojom::WindowFeatures& window_features,
    bool user_gesture,
    bool* was_blocked) {
  return nullptr;
}
```

