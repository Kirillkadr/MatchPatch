### match
```cpp
...
 
 namespace syncer { ... 
 
 void SyncAuthManager::SetLastAuthError(const GoogleServiceAuthError& error) { ... 
last_auth_error_time_ = base::Time::Now();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// We want to override this in BraveSyncAuthManager, but for the base
// implementation fall back onto the anonymous function.
SyncAccountInfo SyncAuthManager::DetermineAccountToUse(
    const signin::IdentityManager* identity_manager) const {
  return syncer::DetermineAccountToUse(identity_manager);
}

```

