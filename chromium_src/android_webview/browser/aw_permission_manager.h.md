### match
```
...
 # ifndef ... 
 namespace android_webview { ... 
 class AwPermissionManager : public content::PermissionControllerDelegate { ... 
 const url::Origin& requesting_origin 
 ) 
 override 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```
  void SetOriginCanReadEnumerateDevicesAudioLabels_ChromiumImpl(
      const url::Origin& origin, bool audio);
  void SetOriginCanReadEnumerateDevicesVideoLabels_ChromiumImpl(
      const url::Origin& origin, bool video);                    

```

