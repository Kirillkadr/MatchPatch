### match
```cpp
...
 
 # ifndef ...   >>> 
 class 
 ChromeBrowserFieldTrials 
 : public variations::PlatformFieldTrials 
 {  <<< 
public
 ... } ...  
```
### patch
```cpp
class ChromeBrowserFieldTrialsChromium : public variations::PlatformFieldTrials {

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ChromeBrowserFieldTrialsChromium : public variations::PlatformFieldTrials { ...   >>> 
 explicit ChromeBrowserFieldTrials(PrefService* local_state);  <<< 
ChromeBrowserFieldTrials(const ChromeBrowserFieldTrials&) = delete;
 ... } ...  
```
### patch
```cpp
  explicit ChromeBrowserFieldTrialsChromium(PrefService* local_state);

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ChromeBrowserFieldTrialsChromium : public variations::PlatformFieldTrials { ... 
explicit ChromeBrowserFieldTrialsChromium(PrefService* local_state);  >>> 
 ChromeBrowserFieldTrials(const ChromeBrowserFieldTrials&) = delete; 
 ChromeBrowserFieldTrials& operator=(const ChromeBrowserFieldTrials&) = delete; 
 ~ChromeBrowserFieldTrials() override;  <<< 
// variations::PlatformFieldTrials:
 ... } ...  
```
### patch
```cpp
  ChromeBrowserFieldTrialsChromium(const ChromeBrowserFieldTrialsChromium&) = delete;
  ChromeBrowserFieldTrialsChromium& operator=(const ChromeBrowserFieldTrialsChromium&) = delete;

  ~ChromeBrowserFieldTrialsChromium() override;

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ChromeBrowserFieldTrialsChromium : public variations::PlatformFieldTrials { ... 
const raw_ptr<PrefService, AcrossTasksDanglingUntriaged> local_state_;
 } 
 ; 
 >>> 
 ... 
```
### patch
```cpp
class ChromeBrowserFieldTrials : public ChromeBrowserFieldTrialsChromium {
 public:
  using ChromeBrowserFieldTrialsChromium::ChromeBrowserFieldTrialsChromium;
  ~ChromeBrowserFieldTrials() override = default;

  // ChromeBrowserFieldTrialsChromium overrides:
  void SetUpClientSideFieldTrials(
      bool has_seed,
      const variations::EntropyProviders& entropy_providers,
      base::FeatureList* feature_list) override;
};


```

