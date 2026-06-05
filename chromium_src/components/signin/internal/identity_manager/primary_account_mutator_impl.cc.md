### match
```cpp
...
 
 namespace signin { ... 
>>> 
 void 
 PrimaryAccountMutatorImpl::RevokeSyncConsent 
 ( 
<<< 
signin_metrics::ProfileSignout source_metric
 ... ) ...  } ...  
```
### patch
```cpp
void PrimaryAccountMutatorImpl::RevokeSyncConsent_ChromiumImpl(

```

### match
```cpp
...
 
 namespace signin { ... 
 
 void PrimaryAccountMutatorImpl::RevokeSyncConsent_ChromiumImpl(
	signin_metrics::ProfileSignout source_metric) { ... 
DCHECK(primary_account_manager_->HasPrimaryAccount(ConsentLevel::kSync));
>>> 
 primary_account_manager_->RevokeSyncConsent(source_metric); 
<<< 
...} ...  } ...  
```
### patch
```cpp
  primary_account_manager_->RevokeSyncConsent_ChromiumImpl(source_metric);

```

### match
```cpp
...
 
 namespace signin { ... 
bool PrimaryAccountMutatorImpl::RemovePrimaryAccountButKeepTokens(
    signin_metrics::ProfileSignout source_metric) {
  if (!primary_account_manager_->HasPrimaryAccount(ConsentLevel::kSignin)) {
    return false;
  }

  primary_account_manager_->RemovePrimaryAccountButKeepTokens(source_metric);
  return true;
}
 #endif 
 // !BUILDFLAG(IS_CHROMEOS) 
 >>> 
 ... } ...  
```
### patch
```cpp
void PrimaryAccountMutatorImpl::RevokeSyncConsent(
    signin_metrics::ProfileSignout source_metric) {}

```

