### match
```cpp
...
 
 # ifndef ...   >>> 
 class 
 HatsServiceAndroid 
 : public HatsService 
 {  <<< 
public
 ... } ...
```
### patch
```cpp
class HatsServiceAndroid_ChromiumImpl : public HatsService {

```

### match
```cpp
...
   >>> 
 DelayedSurveyTask 
 ( 
 HatsServiceAndroid* hats_service 
 ,  <<< ...
```
### patch
```cpp
DelayedSurveyTask(HatsServiceAndroid_ChromiumImpl* hats_service,

```

### match
```cpp
...
 
 # ifndef ... 
 
 class HatsServiceAndroid_ChromiumImpl : public HatsService { ... 
 
 class DelayedSurveyTask : public content::WebContentsObserver { ...   >>> 
 bool 
 operator<(const HatsServiceAndroid::DelayedSurveyTask& other) const 
 {  <<< 
return trigger_ < other.trigger_ ? true
                                       : web_contents() < other.web_contents();
 ... } ...  } ...  } ...  
```
### patch
```cpp
    bool operator<(const HatsServiceAndroid_ChromiumImpl::DelayedSurveyTask& other) const {

```

### match
```cpp
...
 
 # ifndef ... 
bool survey_launched_ = false;  >>> 
 raw_ptr<HatsServiceAndroid> hats_service_;  <<< 
std::unique_ptr<messages::MessageWrapper> message_;
 ... 
```
### patch
```cpp
    raw_ptr<HatsServiceAndroid_ChromiumImpl> hats_service_;

```

### match
```cpp
...
 
 # ifndef ... 
 
 class HatsServiceAndroid_ChromiumImpl : public HatsService { ... 
enum class ShouldShowSurveyReasonsAndroid {
    kYes = 0,
    kAndroidUnknown = 1,   // Catch all for Android invitation dismissals.
                           // Should be investigated if this regularly occurs.
    kAndroidAccepted = 2,  // Invitation accepted
    kAndroidSecondaryAction =
        3,  // Not in use by the default survey implementation. May be used by
            // customized trigger implementations.
    kAndroidExpired = 4,  // Survey invitation expired and was automatically
                          // dismissed. Default timeout is 10s, see
                          // `ChromeMessageAutodismissDurationProvider.java`
    kAndroidDismissedByGesture = 5,  // Dismissed by swiping the dialog away
    kAndroidTabSwitched = 6,
    kAndroidTabDestroyed = 7,
    kAndroidActivityDestroyed = 8,
    kAndroidScopeDestroyed = 9,
    kAndroidDismissedByFeature =
        10,  // Another survey was already launched, leading to the current one
             // being aborted.
    kAndroidCloseButton =
        11,  // Dismissed when a mouse clicks on the close button.
    kMaxValue = kAndroidCloseButton,
  };  >>> 
 explicit HatsServiceAndroid(Profile* profile);  <<< 
HatsServiceAndroid(const HatsServiceAndroid&) = delete;
 ... } ...  
```
### patch
```cpp
  explicit HatsServiceAndroid_ChromiumImpl(Profile* profile);

```

### match
```cpp
...
 
 # ifndef ... 
 
 class HatsServiceAndroid_ChromiumImpl : public HatsService { ... 
explicit HatsServiceAndroid_ChromiumImpl(Profile* profile);  >>> 
 HatsServiceAndroid(const HatsServiceAndroid&) = delete; 
 HatsServiceAndroid& operator=(const HatsServiceAndroid&) = delete; 
 ~HatsServiceAndroid() override;  <<< 
void LaunchSurvey(const std::string& trigger,
                    base::OnceClosure success_callback,
                    base::OnceClosure failure_callback,
                    const SurveyBitsData& product_specific_bits_data,
                    const SurveyStringData& product_specific_string_data,
                    const std::optional<std::string>& supplied_trigger_id,
                    const SurveyOptions& survey_options) override;
 ... } ...  
```
### patch
```cpp
  HatsServiceAndroid_ChromiumImpl(const HatsServiceAndroid_ChromiumImpl&) = delete;
  HatsServiceAndroid_ChromiumImpl& operator=(const HatsServiceAndroid_ChromiumImpl&) = delete;

  ~HatsServiceAndroid_ChromiumImpl() override;

```

### match
```cpp
...
 
 # ifndef ... 
std::set<DelayedSurveyTask> pending_tasks_;  >>> 
 base::WeakPtrFactory<HatsServiceAndroid> weak_ptr_factory_{this};  <<<  ...
```
### patch
```cpp
  base::WeakPtrFactory<HatsServiceAndroid_ChromiumImpl> weak_ptr_factory_{this};

```

### match
```cpp
...
 #endif 
 // CHROME_BROWSER_UI_ANDROID_HATS_HATS_SERVICE_ANDROID_H_ 
 >>> 
 ... 
```
### patch
```cpp

class HatsServiceAndroid : public HatsServiceAndroid_ChromiumImpl {
 public:
  explicit HatsServiceAndroid(Profile* profile);
  HatsServiceAndroid(const HatsServiceAndroid&) = delete;
  HatsServiceAndroid& operator=(const HatsServiceAndroid&) = delete;

  ~HatsServiceAndroid() override;

  bool CanShowSurvey(const std::string& trigger) const override;
};
```

