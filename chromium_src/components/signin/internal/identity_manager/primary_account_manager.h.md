### match
```cpp
...
 
 class PrimaryAccountManager : public ProfileOAuth2TokenServiceObserver { ... 
// Rovokes the sync consent but leaves the primary account and the rest of
 // the accounts untouched. 
 >>> 
void RevokeSyncConsent(signin_metrics::ProfileSignout signout_source_metric);
 ... } ...  
```
### patch
```cpp
  void RevokeSyncConsent_ChromiumImpl(                            
      signin_metrics::ProfileSignout signout_source_metric);

```

