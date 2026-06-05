### match
```cpp
...
 
 namespace syncer { ... 
 
 BASE_FEATURE ( ... 
kSyncFixWebSigninSessionDurationForShortLivedSessions,
             
 base::FEATURE_DISABLED_BY_DEFAULT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kSyncAutofillLoyaltyCard, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

