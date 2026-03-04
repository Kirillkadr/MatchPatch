### match
```
...
#include "base/metrics/field_trial_params.h"

 #include "base/strings/string_number_conversions.h"
 
 >>> 
#include "chrome/browser/download/android/jni_headers/MimeUtils_jni.h"

 ... 
```
### patch
```
#include "brave/browser/download/android/jni_headers/BraveMimeUtils_jni.h"

```

### match
```
...
 namespace 
 { 
 >>> 
// If received bytes is more than the size limit and resumption will restart
 ... } ...  
```
### patch
```
// We need this just to avoid unused function
// 'Java_MimeUtils_canAutoOpenMimeType' error message.
bool DummyMimeUtilUsage() {
  JNIEnv* env = nullptr;
  if (Java_MimeUtils_canAutoOpenMimeType(env, "")) {
    return true;
  }

  return DummyMimeUtilUsage();
}


```

### match
```
...
 
 bool DownloadUtils::ShouldAutoOpenDownload(download::DownloadItem* item) { ...   >>> 
 return 
 Java_MimeUtils_canAutoOpenMimeType(env, item->GetMimeType()) 
 &&  <<< 
IsDownloadUserInitiated(item)
 ... } ...  
```
### patch
```
  return Java_BraveMimeUtils_canAutoOpenMimeType(env, item->GetMimeType()) &&

```

