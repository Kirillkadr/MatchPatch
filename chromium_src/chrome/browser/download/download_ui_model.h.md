### match
```
...
 
 # ifndef ... 
 
 class DownloadUIModel { ... 
// of this method will be different from DownloadItem::OpenDownload() if
 // ShouldPreferOpeningInBrowser(). 
 >>> 
virtual void OpenUsingPlatformHandler();
 ... } ...  
```
### patch
```
  virtual void DeleteLocalFile() {}
  virtual void CopyDownloadLinkToClipboard() {} 

```

