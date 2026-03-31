### match
```cpp
...
 
 # ifndef ... 
 
 namespace speech { ... 
 
 class ChromeSpeechRecognitionManagerDelegate
    : public content::SpeechRecognitionManagerDelegate,
      public content::SpeechRecognitionEventListener { ... 
// Checks for mojom::ViewType::kTabContents host in the UI thread and notifies
 // back the result in the IO thread through |callback|. 
 >>> 
static void CheckRenderFrameType(
      base::OnceCallback<void(bool ask_user, bool is_allowed)> callback,
      int render_process_id,
      int render_frame_id);
 ... } ...  } ...  
```
### patch
```cpp
  static void CheckRenderFrameType_ChromiumImpl(                                     
      base::OnceCallback<void(bool ask_user, bool is_allowed)> callback,
      int render_process_id, int render_frame_id);

```

