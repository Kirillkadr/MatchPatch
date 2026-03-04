### match
```
...
using blink::mojom::FileChooserParams;
 using content::WebContents; 
 >>> 
namespace android_webview {
...
}
 ... 
```
### patch
```
namespace content {
class RenderFrameHost;
}

namespace url {
class Origin;
}


```

### match
```
...
 namespace 
 android_webview 
 { 
 >>> 
AwWebContentsDelegate::AwWebContentsDelegate(
    JNIEnv* env,
    const jni_zero::JavaRef<jobject>& obj)
    : WebContentsDelegateAndroid(env, obj), is_fullscreen_(false) {}
 ... } ...  
```
### patch
```
bool AwWebContentsDelegate::CheckMediaAccessPermission(
    content::RenderFrameHost* render_frame_host,
    const url::Origin& security_origin,
    blink::mojom::MediaStreamType type) {
  return false;
}


```

### match
```
...
 namespace android_webview { ... 
  >>> 
 bool 
 AwWebContentsDelegate::CheckMediaAccessPermission 
 (  <<< ... ) {
  WebContents* web_contents =
      WebContents::FromRenderFrameHost(render_frame_host);
  if (!web_contents) {
    return false;
  }
  AwSettings* aw_settings = AwSettings::FromWebContents(web_contents);
  if (!aw_settings->GetAllowFileAccessFromFileURLs() &&
      security_origin.scheme() == url::kFileScheme) {
    return false;
  }
  AwPermissionManager* pm = AwBrowserContext::FromWebContents(web_contents)
                                ->GetPermissionControllerDelegate();
  switch (type) {
    case blink::mojom::MediaStreamType::DEVICE_AUDIO_CAPTURE:
      return pm->ShouldShowEnumerateDevicesAudioLabels(security_origin);
    case blink::mojom::MediaStreamType::DEVICE_VIDEO_CAPTURE:
      return pm->ShouldShowEnumerateDevicesVideoLabels(security_origin);
    default:
      return false;
  }
}
 ...  } ...  
```
### patch
```
bool AwWebContentsDelegate::CheckMediaAccessPermission_ChromiumImpl(

```

