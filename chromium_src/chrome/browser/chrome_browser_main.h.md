### match
```cpp
...
 
 # ifndef ...   >>> 
 class 
 ChromeBrowserMainParts 
 : public content::BrowserMainParts 
 {  <<< 
public
 ... } ...  
```
### patch
```cpp
class ChromeBrowserMainParts_ChromiumImpl : public content::BrowserMainParts {

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ChromeBrowserMainParts_ChromiumImpl : public content::BrowserMainParts { ... 
static std::unique_ptr<content::BrowserMainParts> Create(
      bool is_integration_test,
      StartupData* startup_data,
      base::OnceClosure threads_ready_closure);  >>> 
 ChromeBrowserMainParts(const ChromeBrowserMainParts&) = delete; 
 ChromeBrowserMainParts& operator=(const ChromeBrowserMainParts&) = delete; 
 ~ChromeBrowserMainParts() override;  <<< 
// Add additional ChromeBrowserMainExtraParts.
 ... } ...  
```
### patch
```cpp
  ChromeBrowserMainParts_ChromiumImpl(const ChromeBrowserMainParts_ChromiumImpl&) = delete;
  ChromeBrowserMainParts_ChromiumImpl& operator=(const ChromeBrowserMainParts_ChromiumImpl&) = delete;
  ~ChromeBrowserMainParts_ChromiumImpl() override;

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ChromeBrowserMainParts_ChromiumImpl : public content::BrowserMainParts { ...   >>> 
 ChromeBrowserMainParts(bool is_integration_test, StartupData* startup_data);  <<< 
// content::BrowserMainParts overrides.
 ... } ...  
```
### patch
```cpp
  ChromeBrowserMainParts_ChromiumImpl(bool is_integration_test, StartupData* startup_data);

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ChromeBrowserMainParts_ChromiumImpl : public content::BrowserMainParts { ... 
#if BUILDFLAG(IS_MAC) || BUILDFLAG(IS_ANDROID) || BUILDFLAG(IS_WIN)
  // Applies enterprise policies for platform auth SSO.
  std::unique_ptr<PlatformAuthPolicyObserver> platform_auth_policy_observer_;
#endif
 } 
 ; 
 >>> 
 ... 
```
### patch
```cpp
class ChromeBrowserMainParts : public ChromeBrowserMainParts_ChromiumImpl {
 public:
  ChromeBrowserMainParts(bool is_integration_test, StartupData* startup_data);

  ChromeBrowserMainParts(const ChromeBrowserMainParts&) = delete;
  ChromeBrowserMainParts& operator=(const ChromeBrowserMainParts&) = delete;
  ~ChromeBrowserMainParts() override;

  int PreMainMessageLoopRun() override;
  void PreBrowserStart() override;
  void PostBrowserStart() override;
  void PreShutdown() override;
  void PreProfileInit() override;
  void PostProfileInit(Profile* profile, bool is_initial_profile) override;

 private:
  friend class ChromeBrowserMainExtraPartsTor;
};


```

