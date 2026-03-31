### match
```cpp
...
>>>
 ChromeBrowserFieldTrials::ChromeBrowserFieldTrials(PrefService* local_state)  <<< 
: local_state_(local_state)
 ...
```
### patch
```cpp
ChromeBrowserFieldTrialsChromium::ChromeBrowserFieldTrialsChromium(PrefService* local_state)

```

### match
```cpp
...
>>>
 local_state_(local_state) 
 {  <<< 
DCHECK(local_state_);
 ... } ...
```
### patch
```cpp
: local_state_(local_state) {

```

### match
```cpp
...
ChromeBrowserFieldTrialsChromium::ChromeBrowserFieldTrialsChromium(PrefService* local_state)
     : local_state_(local_state) {
DCHECK(local_state_);
}  >>> 
 ChromeBrowserFieldTrials::~ChromeBrowserFieldTrials() = default;  <<< 

 ...
```
### patch
```cpp
ChromeBrowserFieldTrialsChromium::~ChromeBrowserFieldTrialsChromium() = default;

```

### match
```cpp
...
>>>
 void 
 ChromeBrowserFieldTrials::SetUpClientSideFieldTrials 
 (  <<< 
bool has_seed
 ... ) ...  
```
### patch
```cpp

void ChromeBrowserFieldTrialsChromium::SetUpClientSideFieldTrials(

```

### match
```cpp
...
>>>
 void 
 ChromeBrowserFieldTrials::RegisterSyntheticTrials() 
 {  <<< 
#if BUILDFLAG(IS_ANDROID)
  {
    auto trial_info =
        base::android::BackgroundThreadPoolFieldTrial::GetTrialInfo();
    if (trial_info.has_value()) {
      // The annotation mode is set to |kCurrentLog| since the field trial has
      // taken effect at process startup.
      ChromeMetricsServiceAccessor::RegisterSyntheticFieldTrial(
          trial_info->trial_name, trial_info->group_name,
          variations::SyntheticTrialAnnotationMode::kCurrentLog);
    }
  }
#endif
 ... } ...  
```
### patch
```cpp
void ChromeBrowserFieldTrialsChromium::RegisterSyntheticTrials() {

```

### match
```cpp
...
>>>
 void 
 ChromeBrowserFieldTrials::RegisterFeatureOverrides 
 (  <<< 
base::FeatureList* feature_list
 ... ) ...  
```
### patch
```cpp
void ChromeBrowserFieldTrialsChromium::RegisterFeatureOverrides(

```

### match
```cpp
...
 
 void ChromeBrowserFieldTrialsChromium::RegisterFeatureOverrides(
base::FeatureList* feature_list) { ... 
// BUILDFLAG(IS_ANDROID)
 } 
 >>> 
 ... 
```
### patch
```cpp
void ChromeBrowserFieldTrials::SetUpClientSideFieldTrials(
    bool has_seed,
    const variations::EntropyProviders& entropy_providers,
    base::FeatureList* feature_list) {
  // Don't setup upstream's client-side field trials.
}

```

