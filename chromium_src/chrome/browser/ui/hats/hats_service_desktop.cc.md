### match
```cpp
...
>>>
 HatsServiceDesktop::DelayedSurveyTask::DelayedSurveyTask 
 ( 
 HatsServiceDesktop* hats_service 
 ,  <<< 
std::string trigger
 ... ) ...
```
### patch
```cpp
HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask::DelayedSurveyTask(
    HatsServiceDesktop_ChromiumImpl* hats_service,

```

### match
```cpp
...
HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask::DelayedSurveyTask(
    HatsServiceDesktop_ChromiumImpl* hats_service,
std::string trigger,
    content::WebContents* web_contents,
    const SurveyBitsData& product_specific_bits_data,
    const SurveyStringData& product_specific_string_data,
    NavigationBehavior navigation_behavior,
    base::OnceClosure success_callback,
    base::OnceClosure failure_callback,
    std::optional<std::string_view> supplied_trigger_id)
    : hats_service_(hats_service),
      trigger_(trigger),
      product_specific_bits_data_(product_specific_bits_data),
      product_specific_string_data_(product_specific_string_data),
      navigation_behavior_(navigation_behavior),
      success_callback_(std::move(success_callback)),
      failure_callback_(std::move(failure_callback)),
      supplied_trigger_id_(std::move(supplied_trigger_id)) {
  Observe(web_contents);
}  >>> 
 HatsServiceDesktop::DelayedSurveyTask::~DelayedSurveyTask() = default;  <<< 
base::WeakPtr<HatsServiceDesktop::DelayedSurveyTask>
HatsServiceDesktop::DelayedSurveyTask::GetWeakPtr() {
  return weak_ptr_factory_.GetWeakPtr();
}
 ...
```
### patch
```cpp
HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask::~DelayedSurveyTask() = default;

```

### match
```cpp
...
>>>
 base::WeakPtr<HatsServiceDesktop::DelayedSurveyTask> 
 HatsServiceDesktop::DelayedSurveyTask::GetWeakPtr() 
 {  <<< 
return weak_ptr_factory_.GetWeakPtr();
 ... } ...
```
### patch
```cpp
base::WeakPtr<HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask>
HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask::GetWeakPtr() {

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::DelayedSurveyTask::Launch() 
 {  <<< 
 ... } ...
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask::Launch() {

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::DelayedSurveyTask::DidFinishNavigation 
 (  <<< 
content::NavigationHandle* navigation_handle
 ... ) ...
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask::DidFinishNavigation(

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::DelayedSurveyTask::WebContentsDestroyed() 
 {  <<< 
if (!failure_callback_.is_null()) {
    std::move(failure_callback_).Run();
  }
 ... } ...
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask::WebContentsDestroyed() {

```

### match
```cpp
...
>>>
 HatsServiceDesktop::HatsServiceDesktop(Profile* profile)  <<< 
: HatsService(profile)
 ...
```
### patch
```cpp
HatsServiceDesktop_ChromiumImpl::HatsServiceDesktop_ChromiumImpl(Profile* profile)

```

### match
```cpp
...
HatsServiceDesktop_ChromiumImpl::HatsServiceDesktop_ChromiumImpl(Profile* profile)  >>> 
 HatsService(profile) {}  <<< 
HatsServiceDesktop::~HatsServiceDesktop() = default;
 ...
```
### patch
```cpp
: HatsService(profile) {}

```

### match
```cpp
...
HatsServiceDesktop_ChromiumImpl::HatsServiceDesktop_ChromiumImpl(Profile* profile)
     : HatsService(profile) {}  >>> 
 HatsServiceDesktop::~HatsServiceDesktop() = default;  <<< 
// static
 ...
```
### patch
```cpp
HatsServiceDesktop_ChromiumImpl::~HatsServiceDesktop_ChromiumImpl() = default;


```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::RegisterProfilePrefs 
 (  <<< 
user_prefs::PrefRegistrySyncable* registry
 ... ) ...
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::RegisterProfilePrefs(

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::LaunchSurvey 
 (  <<< 
const std::string& trigger
 ... ) ...
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::LaunchSurvey(

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::LaunchSurveyForWebContents 
 (  <<< 
const std::string& trigger
 ... ) ...
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::LaunchSurveyForWebContents(

```

### match
```cpp
...
>>>
 bool 
 HatsServiceDesktop::LaunchDelayedSurvey 
 (  <<< 
const std::string& trigger
 ... ) ...
```
### patch
```cpp
bool HatsServiceDesktop_ChromiumImpl::LaunchDelayedSurvey(

```

### match
```cpp
...
>>>
 void 
 (HatsServiceDesktop::*launch_survey) 
 (  <<< 
const std::string&
 ... ) ...
```
### patch
```cpp
void (HatsServiceDesktop_ChromiumImpl::*launch_survey)(

```

### match
```cpp
...
 
 bool HatsServiceDesktop_ChromiumImpl::LaunchDelayedSurvey(
const std::string& trigger,
    int timeout_ms,
    const SurveyBitsData& product_specific_bits_data,
    const SurveyStringData& product_specific_string_data) { ...   >>> 
 &HatsServiceDesktop::LaunchSurvey 
 ;  <<<  ...} ...
```
### patch
```cpp
&HatsServiceDesktop_ChromiumImpl::LaunchSurvey;

```

### match
```cpp
...
>>>
 bool 
 HatsServiceDesktop::LaunchDelayedSurveyForWebContents 
 (  <<< 
const std::string& trigger
 ... ) ...
```
### patch
```cpp
bool HatsServiceDesktop_ChromiumImpl::LaunchDelayedSurveyForWebContents(

```

### match
```cpp
...   >>> 
 base::BindOnce 
 ( 
 &HatsServiceDesktop::DelayedSurveyTask::Launch 
 , 
 const_cast<HatsServiceDesktop::DelayedSurveyTask&> 
 (  <<< 
...
```
### patch
```cpp
base::BindOnce(&HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask::Launch,
                         const_cast<HatsServiceDesktop_ChromiumImpl::DelayedSurveyTask&>(

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::SetSurveyMetadataForTesting 
 (  <<< 
const HatsService::SurveyMetadata& metadata
 ... ) ...  
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::SetSurveyMetadataForTesting(

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::GetSurveyMetadataForTesting 
 (  <<< 
HatsService::SurveyMetadata* metadata
 ... ) ...  
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::GetSurveyMetadataForTesting(

```

### match
```cpp
...
>>>
 bool 
 HatsServiceDesktop::HasPendingTasks() 
 {  <<< 
return !pending_tasks_.empty();
 ... } ...  
```
### patch
```cpp
bool HatsServiceDesktop_ChromiumImpl::HasPendingTasks() {

```

### match
```cpp
...
>>>
 bool 
 HatsServiceDesktop::CanShowSurvey(const std::string& trigger) const 
 {  <<< 
// Survey should not be loaded if the corresponding survey config is
 ... } ...  
```
### patch
```cpp
bool HatsServiceDesktop_ChromiumImpl::CanShowSurvey(const std::string& trigger) const {

```

### match
```cpp
...
 
 bool HatsServiceDesktop_ChromiumImpl::CanShowSurvey(const std::string& trigger) const { ... 
 
 if (DoesCooldownApply(profile(), GetPrefsForHatsMetadata(), config)) { ... 
 
 UMA_HISTOGRAM_ENUMERATION ( ...   >>> 
 HatsServiceDesktop::ShouldShowSurveyReasons::kNoAnyLastSurveyTooRecent 
 ) 
 ;  <<<  ...} ...  } ...  
```
### patch
```cpp
        HatsServiceDesktop_ChromiumImpl::ShouldShowSurveyReasons::kNoAnyLastSurveyTooRecent);

```

### match
```cpp
...
>>>
 bool 
 HatsServiceDesktop::CanShowAnySurvey(bool user_prompted) const 
 {  <<< 
// HaTS requires metrics consent to run. This is also how HaTS can be
 ... } ...  
```
### patch
```cpp
bool HatsServiceDesktop_ChromiumImpl::CanShowAnySurvey(bool user_prompted) const {

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::RecordSurveyAsShown(std::string trigger_id) 
 {  <<< 
// Record the trigger associated with the trigger_id. This is recorded
 ... } ...  
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::RecordSurveyAsShown(std::string trigger_id) {

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::HatsNextDialogClosed() 
 {  <<< 
hats_next_dialog_exists_ = false;
 ... } ...  
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::HatsNextDialogClosed() {

```

### match
```cpp
...
>>>
 PrefService 
 * HatsServiceDesktop::GetPrefsForHatsMetadata() const 
 {  <<< 
// Make sure we persist HaTS metadata to the original profile, otherwise HaTS
 ... } ...  
```
### patch
```cpp
PrefService* HatsServiceDesktop_ChromiumImpl::GetPrefsForHatsMetadata() const {

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::RemoveTask(const DelayedSurveyTask& task) 
 {  <<< 
pending_tasks_.erase(task);
 ... } ...  
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::RemoveTask(const DelayedSurveyTask& task) {

```

### match
```cpp
...
>>>
 bool 
 HatsServiceDesktop::ShouldShowSurvey(const std::string& trigger) const 
 {  <<< 
if (!CanShowSurvey(trigger)) {
    return false;
  }
 ... } ...  
```
### patch
```cpp
bool HatsServiceDesktop_ChromiumImpl::ShouldShowSurvey(const std::string& trigger) const {

```

### match
```cpp
...
>>>
 bool 
 HatsServiceDesktop::IsRightBrowserType 
 (  <<< 
Browser* browser
 ... ) ...  
```
### patch
```cpp
bool HatsServiceDesktop_ChromiumImpl::IsRightBrowserType(

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::LaunchSurveyForBrowser 
 (  <<< 
Browser* browser
 ... ) ...  
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::LaunchSurveyForBrowser(

```

### match
```cpp
...
>>>
 void 
 HatsServiceDesktop::CheckSurveyStatusAndMaybeShow 
 (  <<< 
Browser* browser
 ... ) ...  
```
### patch
```cpp
void HatsServiceDesktop_ChromiumImpl::CheckSurveyStatusAndMaybeShow(

```

### match
```cpp
...
 
 void HatsServiceDesktop_ChromiumImpl::CheckSurveyStatusAndMaybeShow(
Browser* browser,
    const std::string& trigger,
    base::OnceClosure success_callback,
    base::OnceClosure failure_callback,
    const SurveyBitsData& product_specific_bits_data,
    const SurveyStringData& product_specific_string_data,
    const std::optional<std::string_view>& supplied_trigger_id) { ... 
hats_next_dialog_exists_ = true;
 } 
 >>> 
 ... 
```
### patch
```cpp
HatsServiceDesktop::HatsServiceDesktop(Profile* profile)
    : HatsServiceDesktop_ChromiumImpl(profile) {}

HatsServiceDesktop::~HatsServiceDesktop() = default;

bool HatsServiceDesktop::CanShowSurvey(const std::string& trigger) const {
  return false;
}

```

