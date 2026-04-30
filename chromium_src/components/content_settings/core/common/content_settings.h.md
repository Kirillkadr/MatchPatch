### match
```cpp
...
 
 # ifndef ...   >>> 
 struct 
 RendererContentSettingRules 
 {  <<< 
// Returns true if |content_type| is a type that is contained in this class.
 ... } ...  
```
### patch
```cpp
struct RendererContentSettingRules_ChromiumImpl {

```

### match
```cpp
...
 
 # ifndef ... 
void FilterRulesByOutermostMainFrameURL(const GURL& outermost_main_frame_url);  >>> 
 RendererContentSettingRules(); 
 ~RendererContentSettingRules(); 
 RendererContentSettingRules(const RendererContentSettingRules& rules); 
 RendererContentSettingRules(RendererContentSettingRules&& rules); 
 RendererContentSettingRules& operator=(
      const RendererContentSettingRules& rules); 
 RendererContentSettingRules& operator=(RendererContentSettingRules&& rules);  <<< 
bool operator==(const RendererContentSettingRules& other) const;
 ... 
```
### patch
```cpp
  RendererContentSettingRules_ChromiumImpl();
  ~RendererContentSettingRules_ChromiumImpl();
  RendererContentSettingRules_ChromiumImpl(const RendererContentSettingRules_ChromiumImpl& rules);
  RendererContentSettingRules_ChromiumImpl(RendererContentSettingRules_ChromiumImpl&& rules);
  RendererContentSettingRules_ChromiumImpl& operator=(
      const RendererContentSettingRules_ChromiumImpl& rules);
  RendererContentSettingRules_ChromiumImpl& operator=(RendererContentSettingRules_ChromiumImpl&& rules);

```

### match
```cpp
...
 
 # ifndef ... 
RendererContentSettingRules_ChromiumImpl& operator=(RendererContentSettingRules_ChromiumImpl&& rules);  >>> 
 bool operator==(const RendererContentSettingRules& other) const;  <<< 
ContentSettingsForOneType mixed_content_rules;
 ... 
```
### patch
```cpp

  bool operator==(const RendererContentSettingRules_ChromiumImpl& other) const;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ...   >>> 
 kTpcdGrant 
 ,  <<< 
kOsJavascriptOptimizer
 ... } ...  
```
### patch
```cpp
  kTpcdGrant, kRemoteList,

```

### match
```cpp
...
 
 namespace content_settings { ... 
 
 constexpr SettingSource GetSettingSourceFromProviderType(
    ProviderType provider_type) { ... 
 
 case ProviderType : ... 
 return SettingSource::kOsJavascriptOptimizer; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
    case ProviderType::kRemoteListProvider:
  return SettingSource::kRemoteList;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
constexpr SettingSource GetSettingSourceFromProviderType(
    ProviderType provider_type) {
  switch (provider_type) {
    case ProviderType::kWebuiAllowlistProvider:
    case ProviderType::kComponentExtensionProvider:
      return SettingSource::kAllowList;
    case ProviderType::kPolicyProvider:
      return SettingSource::kPolicy;
    case ProviderType::kSupervisedProvider:
      return SettingSource::kSupervised;
    case ProviderType::kCustomExtensionProvider:
    case ProviderType::kExtensionInstallTimePermissionProvider:
      return SettingSource::kExtension;
    case ProviderType::kInstalledWebappProvider:
      return SettingSource::kInstalledWebApp;
    case ProviderType::kJavascriptOptimizerAndroidProvider:
      return SettingSource::kOsJavascriptOptimizer;
        case ProviderType::kRemoteListProvider:
			  return SettingSource::kRemoteList;
			case ProviderType::kNotificationAndroidProvider:
    case ProviderType::kOneTimePermissionProvider:
    case ProviderType::kPrefProvider:
    case ProviderType::kDefaultProvider:
      return SettingSource::kUser;
    case ProviderType::kProviderForTests:
    case ProviderType::kOtherProviderForTests:
      return SettingSource::kTest;
    case content_settings::ProviderType::kNone:
      return SettingSource::kNone;
  }
}
 } 
 // namespace content_settings 
 >>> 
 ... 
```
### patch
```cpp
struct RendererContentSettingRules
    : public RendererContentSettingRules_ChromiumImpl {
  RendererContentSettingRules();
  ~RendererContentSettingRules();
  RendererContentSettingRules(const RendererContentSettingRules& rules);
  RendererContentSettingRules(RendererContentSettingRules&& rules);
  RendererContentSettingRules& operator=(
      const RendererContentSettingRules& rules);
  RendererContentSettingRules& operator=(RendererContentSettingRules&& rules);
  static bool IsRendererContentSetting(ContentSettingsType content_type);

  void FilterRulesByOutermostMainFrameURL(const GURL& outermost_main_frame_url);

  ContentSettingsForOneType autoplay_rules;
  ContentSettingsForOneType fingerprinting_rules;
  ContentSettingsForOneType brave_shields_rules;
  ContentSettingsForOneType cosmetic_filtering_rules;
  std::map<ContentSettingsType, ContentSettingsForOneType> webcompat_rules;
};

namespace content_settings {

bool IsExplicitSetting(const ContentSettingPatternSource& setting);
bool IsExplicitSetting(const SettingInfo& setting);

}  // namespace content_settings

```

