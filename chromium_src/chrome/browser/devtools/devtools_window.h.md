### match
```
...
 
 # ifndef ... 
friend class DevToolsWindowCreationObserver;
 friend class HatsNextWebDialogBrowserTest; 
 >>> 
using CreationCallback = base::RepeatingCallback<void(DevToolsWindow*)>;
 ... 
```
### patch
```
  friend class TorProfileManagerUnitTest;

```

