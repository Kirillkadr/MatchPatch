### match
```
...
 # ifndef ... 
 namespace android_webview { ... 
 class AwWebContentsDelegate
    : public web_contents_delegate_android::WebContentsDelegateAndroid { ... 
 content::MediaResponseCallback callback 
 ) 
 override 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```
  bool CheckMediaAccessPermission_ChromiumImpl(
      content::RenderFrameHost* render_frame_host,
      const url::Origin& security_origin, blink::mojom::MediaStreamType type);

```

