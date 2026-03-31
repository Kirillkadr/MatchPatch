### match
```cpp
...
 
 namespace content_settings { ... 
 
 void ContentSettingsAgentImpl::ClearBlockedContentSettings() { ... 
cached_storage_permissions_.clear();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
ContentSetting GetContentSettingFromRulesImpl(
    const ContentSettingsForOneType& rules,
    const GURL& secondary_url) {
  return GetContentSettingFromRules(rules, secondary_url);
}
bool ContentSettingsAgentImpl::HasContentSettingsRules() const {
  return content_setting_rules_.get();
}

```

