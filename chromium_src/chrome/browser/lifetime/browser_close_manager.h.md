### match
```
...
 
 # ifndef ... 
// Starts closing all browser windows.
 void StartClosingBrowsers(); 
 >>> 
protected
 ... 
```
### patch
```
  static bool BrowserClosingStarted();
  void StartClosingBrowsers_ChromiumImpl();

```

### match
```
...
 
 # ifndef ... 
// Notifies all browser windows that the close is cancelled.
 void CancelBrowserClose(); 
 >>> 
// Checks whether all browser windows are ready to close and closes them if
 ... 
```
### patch
```
  void CancelBrowserClose_ChromiumImpl();

```

