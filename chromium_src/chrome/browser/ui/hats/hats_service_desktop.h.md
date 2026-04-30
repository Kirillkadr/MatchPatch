### match
```cpp
...
 
 # ifndef ...   >>> 
 class 
 HatsServiceDesktop 
 : public HatsService 
 {  <<< 
public
 ... } ...  
```
### patch
```cpp
class HatsServiceDesktop_ChromiumImpl : public HatsService {

```

### match
```cpp
...
 
 class HatsServiceDesktop_ChromiumImpl : public HatsService { ... 
 
 class DelayedSurveyTask : public content::WebContentsObserver { ...   >>> 
 DelayedSurveyTask 
 ( 
 HatsServiceDesktop* hats_service 
 ,  <<< 
std::string trigger
 ... ) ...  } ...  } ...  
```
### patch
```cpp
    DelayedSurveyTask(HatsServiceDesktop_ChromiumImpl* hats_service,

```

### match
```cpp
...
 
 # ifndef ... 
 
 class HatsServiceDesktop_ChromiumImpl : public HatsService { ... 
 
 class DelayedSurveyTask : public content::WebContentsObserver { ...   >>> 
 bool 
 operator<(const HatsServiceDesktop::DelayedSurveyTask& other) const 
 {  <<< 
return trigger_ < other.trigger_ ? true
                                       : web_contents() < other.web_contents();
 ... } ...  } ...  } ...  
```
### patch
```cpp
    bool operator<(const HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask& other) const {

```

### match
```cpp
...
 
 # ifndef ...   >>> 
 raw_ptr<HatsServiceDesktop> hats_service_;  <<< 
std::string trigger_;
 ... 
```
### patch
```cpp
    raw_ptr<HatsServiceDesktop_ChromiumImpl> hats_service_;

```

### match
```cpp
...
 
 # ifndef ... 
 
 class HatsServiceDesktop_ChromiumImpl : public HatsService { ... 
enum class ShouldShowSurveyReasons {
    kYes = 0,
    kNoOffline = 1,
    kNoLastSessionCrashed = 2,
    kNoReceivedSurveyInCurrentMilestone = 3,
    kNoProfileTooNew = 4,
    kNoLastSurveyTooRecent = 5,
    kNoBelowProbabilityLimit = 6,
    kNoTriggerStringMismatch = 7,
    kNoWrongBrowserType = 8,
    kNoIncognitoDisabled = 9,
    kNoCookiesBlocked = 10,            // Unused.
    kNoThirdPartyCookiesBlocked = 11,  // Unused.
    kNoSurveyUnreachable = 12,
    kNoSurveyOverCapacity = 13,
    kNoSurveyAlreadyInProgress = 14,
    kNoAnyLastSurveyTooRecent = 15,
    kNoRejectedByHatsService = 16,
    kNoLastSurveyCheckTooRecent = 17,
    kMaxValue = kNoLastSurveyCheckTooRecent,
  };  >>> 
 explicit HatsServiceDesktop(Profile* profile);  <<< 
HatsServiceDesktop(const HatsServiceDesktop&) = delete;
 ... } ...  
```
### patch
```cpp
  explicit HatsServiceDesktop_ChromiumImpl(Profile* profile);

```

### match
```cpp
...
 
 # ifndef ... 
 
 class HatsServiceDesktop_ChromiumImpl : public HatsService { ... 
explicit HatsServiceDesktop_ChromiumImpl(Profile* profile);  >>> 
 HatsServiceDesktop(const HatsServiceDesktop&) = delete; 
 HatsServiceDesktop& operator=(const HatsServiceDesktop&) = delete; 
 ~HatsServiceDesktop() override;  <<< 
static void RegisterProfilePrefs(user_prefs::PrefRegistrySyncable* registry);
 ... } ...  
```
### patch
```cpp
  HatsServiceDesktop_ChromiumImpl(const HatsServiceDesktop_ChromiumImpl&) = delete;
  HatsServiceDesktop_ChromiumImpl& operator=(const HatsServiceDesktop_ChromiumImpl&) = delete;

  ~HatsServiceDesktop_ChromiumImpl() override;

```

### match
```cpp
...
 
 # ifndef ... 
bool hats_next_dialog_exists_ = false;  >>> 
 base::WeakPtrFactory<HatsServiceDesktop> weak_ptr_factory_{this};  <<<  ...
```
### patch
```cpp
  base::WeakPtrFactory<HatsServiceDesktop_ChromiumImpl> weak_ptr_factory_{this};

```

### match
```cpp
...
 
 # ifndef ... 
 
 class HatsServiceDesktop_ChromiumImpl : public HatsService { ... 
base::WeakPtrFactory<HatsServiceDesktop_ChromiumImpl> weak_ptr_factory_{this};
 } 
 ; 
 >>> 
 ... 
```
### patch
```cpp
class HatsServiceDesktop : public HatsServiceDesktop_ChromiumImpl {
 public:
  explicit HatsServiceDesktop(Profile* profile);
  HatsServiceDesktop(const HatsServiceDesktop&) = delete;
  HatsServiceDesktop& operator=(const HatsServiceDesktop&) = delete;

  ~HatsServiceDesktop() override;

  bool CanShowSurvey(const std::string& trigger) const override;
};

```
