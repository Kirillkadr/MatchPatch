### match
```cpp
...
#include "base/test/scoped_feature_list.h"

 #include "base/time/time.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/test/base/brave_testing_profile.h"

```

### match
```cpp
...
 
 namespace { ...   >>> 
 class 
 PushMessagingTestingProfile 
 : public TestingProfile 
 {  <<< 
public
 ... } ...  } ...  
```
### patch
```cpp
class PushMessagingTestingProfile : public BraveTestingProfile {

```

### match
```cpp
...
>>>
 TEST_F(PushMessagingServiceTest, RecordsRevocationAndSourceUiNoReporterTest) 
 {  <<< 
base::HistogramTester histograms;
 ... } ...  
```
### patch
```cpp
TEST_F(PushMessagingServiceTest, DISABLED_RecordsRevocationAndSourceUiNoReporterTest) {

```

### match
```cpp
...
>>>
 TEST_F(PushMessagingServiceTest, RecordsRevocationAndSourceUiWithReporterTest) 
 {  <<< 
base::HistogramTester histograms;
 ... } ...  
```
### patch
```cpp
TEST_F(PushMessagingServiceTest, DISABLED_RecordsRevocationAndSourceUiWithReporterTest) {

```

### match
```cpp
...
>>>
 TEST_F(PushMessagingServiceTest, ProfileDestructionTest) 
 {  <<< 
PushMessagingServiceImpl* push_service = profile()->GetPushMessagingService();
 ... } ...  
```
### patch
```cpp
TEST_F(PushMessagingServiceTest, DISABLED_ProfileDestructionTest) {

```

### match
```cpp
...
 
 #if BUILDFLAG(IS_ANDROID ) ... 
 
 class FCMRevocationTest : public PushMessagingServiceTest { ... 
 void SetPermission ( ...   >>> 
 TestingProfile* profile 
 ) 
 {  <<< 
HostContentSettingsMap* host_content_settings_map =
        HostContentSettingsMapFactory::GetForProfile(profile);
 ... } ...  } ...  
```
### patch
```cpp
                     BraveTestingProfile* profile) {

```

