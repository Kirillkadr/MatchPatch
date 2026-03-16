### match
```
...
 
 namespace { ... 
 
 void ShowInProgressDownloads(Profile* profile) { ... 
if (download_core_service &&
      download_core_service->BlockingShutdownCount() > 0) {
    chrome::ScopedTabbedBrowserDisplayer displayer(profile);
    chrome::ShowDownloads(displayer.browser());
  }
 } 
 >>> 
 ... } ...  
```
### patch
```
// Whether the browser closing is in-progress or not.
// Introduced this new flag instead of using browser_shutdown::IsTryingToQuit()
// because it returns true when all browser windows are closed on Windows/Linux.
// I assume that the reason is background running on Windows/Linux.
bool g_browser_closing_started = false;


```

### match
```
...
>>>
 void 
 BrowserCloseManager::StartClosingBrowsers() 
 {  <<< 
close_timer_.emplace();
 ... } ...  
```
### patch
```
void BrowserCloseManager::tartClosingBrowsers_ChromiumImpl() {

```

### match
```
...
>>>
 void 
 BrowserCloseManager::CancelBrowserClose() 
 {  <<< 
// This is the abort endpoint. Record the metric if we haven't already.
 ... } ...  
```
### patch
```
void BrowserCloseManager::CancelBrowserClose_ChromiumImpl() {

```

### match
```
...
 
 void BrowserCloseManager::OnBrowserReportCloseable(bool proceed) { ... 
 
 else { ...   >>> 
 CancelBrowserClose();  <<<  ...} ...  } ...  
```
### patch
```
    CancelBrowserClose_ChromiumImpl();

```

### match
```
...
 
 void BrowserCloseManager::OnReportDownloadsCancellable(bool proceed) { ... 
if (proceed) {
    CloseBrowsers();
    return;
  }  >>> 
 CancelBrowserClose();  <<< 
// Open the downloads page for each profile with downloads in progress.
 ... } ...  
```
### patch
```
  CancelBrowserClose_ChromiumImpl();

```

### match
```
...
 
 void BrowserCloseManager::CloseBrowsers() { ... 
#if BUILDFLAG(ENABLE_CHROME_NOTIFICATIONS)
  NotificationUIManager* notification_manager =
      g_browser_process->notification_ui_manager();
  if (notification_manager) {
    notification_manager->CancelAll();
  }
#endif
 } 
 >>> 
 ... 
```
### patch
```

// static
bool BrowserCloseManager::BrowserClosingStarted() {
  return g_browser_closing_started;
}

void BrowserCloseManager::StartClosingBrowsers() {
  g_browser_closing_started = true;
  StartClosingBrowsers_ChromiumImpl();
}

void BrowserCloseManager::CancelBrowserClose() {
  g_browser_closing_started = false;
  CancelBrowserClose_ChromiumImpl();
}
```

