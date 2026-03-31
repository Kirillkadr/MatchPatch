### match
```cpp
...
 
 namespace speech { ...   >>> 
 void 
 ChromeSpeechRecognitionManagerDelegate::CheckRenderFrameType 
 (  <<< 
base::OnceCallback<void(bool ask_user, bool is_allowed)> callback
 ... ) ...  } ...  
```
### patch
```cpp
void ChromeSpeechRecognitionManagerDelegate::CheckRenderFrameType_ChromiumImpl(

```

### match
```cpp
...
 
 namespace speech { ... 
 
 void ChromeSpeechRecognitionManagerDelegate::CheckRenderFrameType_ChromiumImpl(
	base::OnceCallback<void(bool ask_user, bool is_allowed)> callback,
    int render_process_id,
    int render_frame_id) { ... 
content::GetIOThreadTaskRunner({})->PostTask(
      FROM_HERE,
      base::BindOnce(std::move(callback), check_permission, allowed));
 } 
 >>> 
 ... } ...  
```
### patch
```cpp

// static
void ChromeSpeechRecognitionManagerDelegate::CheckRenderFrameType(
    base::OnceCallback<void(bool ask_user, bool is_allowed)> callback,
    int render_process_id,
    int render_frame_id) {
  DCHECK_CURRENTLY_ON(BrowserThread::UI);

  if (auto* rph = content::RenderProcessHost::FromID(render_process_id)) {
    if (auto* profile = Profile::FromBrowserContext(rph->GetBrowserContext())) {
      if (profile->IsTor()) {
        // Disable speech recongition in Tor.
        content::GetIOThreadTaskRunner({})->PostTask(
            FROM_HERE, base::BindOnce(std::move(callback), false, false));
        return;
      }
    }
  }

  return CheckRenderFrameType_ChromiumImpl(std::move(callback),
                                           render_process_id, render_frame_id);
}



```

