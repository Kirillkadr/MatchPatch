### match
```cpp
...
 base::DictValue PasswordStatusCheckService::GetPasswordCardData ( ... 
 bool signed_in 
 ) 
 { 
 >>> 
if (no_passwords_saved()) {
    bool password_saving_allowed = profile_->GetPrefs()->GetBoolean(
        password_manager::prefs::kCredentialsEnableService);
    return GetNoPasswordCardData(password_saving_allowed);
  }
 ... } ...  
```
### patch
```cpp
     base::DictValue dict;
     dict.Set(safety_hub::kCardStateKey,
           static_cast<int>(safety_hub::SafetyHubCardState::kSafe));
     return dict;

```

