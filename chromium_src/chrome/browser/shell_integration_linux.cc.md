### match
```cpp
...
 
 namespace shell_integration { ...   >>> 
 DefaultWebClientState 
 GetDefaultBrowser() 
 {  <<< 
return shell_integration_linux::GetIsDefaultWebClient(std::string());
 ... } ...  } ...  
```
### patch
```cpp
DefaultWebClientState GetDefaultBrowser_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace shell_integration { ... 
 
 namespace internal { ... 
DefaultWebClientSetPermission GetPlatformSpecificDefaultWebClientSetPermission(
    WebClientSetMethod method) {
  return SET_DEFAULT_UNATTENDED;
}
 } 
 // namespace internal 
 >>> 
 ... } ...  
```
### patch
```cpp
bool IsAnyBraveBrowserDefaultBrowser() {
  base::ScopedBlockingCall scoped_blocking_call(FROM_HERE,
                                                base::BlockingType::MAY_BLOCK);

  std::vector<std::string> argv;
  argv.push_back(shell_integration_linux::kXdgSettings);
  argv.push_back("get");
  argv.push_back(shell_integration_linux::kXdgSettingsDefaultBrowser);

  std::string browser;
  // We don't care about the return value here.
  base::GetAppOutput(base::CommandLine(argv), &browser);
  return browser.find("brave-browser") != std::string::npos;
}

DefaultWebClientState GetDefaultBrowser() {
  // Check whether current install is default.
  auto state = GetDefaultBrowser_ChromiumImpl();
  if (state == IS_DEFAULT)
    return state;

  // Check Other channel installs are default.
  return IsAnyBraveBrowserDefaultBrowser() ? OTHER_MODE_IS_DEFAULT
                                           : NOT_DEFAULT;
}


```

