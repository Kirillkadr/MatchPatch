### match
```cpp
...
#include "components/signin/public/base/signin_client.h"

 #include "components/signin/public/base/signin_switches.h"
 
 >>> 
#if BUILDFLAG(IS_ANDROID)
#include "components/signin/internal/identity_manager/profile_oauth2_token_service_delegate_android.h"
#endif
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_DICE_SUPPORT)
#include "brave/components/signin/internal/identity_manager/brave_mutable_profile_oauth2_token_service_delegate.h"
#endif  // BUILDFLAG(ENABLE_DICE_SUPPORT)

```

### match
```cpp
...
 
 namespace { ... 
>>> 
 std::unique_ptr<MutableProfileOAuth2TokenServiceDelegate> 
<<< 
...} ...  
```
### patch
```cpp
std::unique_ptr<BraveMutableProfileOAuth2TokenServiceDelegate>

```

### match
```cpp
...
 
 namespace { ... 
 std::unique_ptr<BraveMutableProfileOAuth2TokenServiceDelegate>
	CreateMutableProfileOAuthDelegate ( ... 
>>> 
 MutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback 
<<< 
...) ...  } ...  
```
### patch
```cpp
    BraveMutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback

```

### match
```cpp
...
 
 namespace { ... 
 
 std::unique_ptr<BraveMutableProfileOAuth2TokenServiceDelegate>
	CreateMutableProfileOAuthDelegate(
    AccountTrackerService* account_tracker_service,
    bool delete_signin_cookies_on_exit,
    scoped_refptr<TokenWebData> token_web_data,
    SigninClient* signin_client,
    unexportable_keys::UnexportableKeyService* unexportable_key_service,
#if BUILDFLAG(IS_WIN)
        BraveMutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback
		reauth_callback,
#endif
    network::NetworkConnectionTracker* network_connection_tracker) { ... 
>>> 
 return 
 std::make_unique<MutableProfileOAuth2TokenServiceDelegate> 
 ( 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
  return std::make_unique<BraveMutableProfileOAuth2TokenServiceDelegate>(

```

### match
```cpp
...
 
 namespace { ... 
 
 std::unique_ptr<BraveMutableProfileOAuth2TokenServiceDelegate>
	CreateMutableProfileOAuthDelegate(
    AccountTrackerService* account_tracker_service,
    bool delete_signin_cookies_on_exit,
    scoped_refptr<TokenWebData> token_web_data,
    SigninClient* signin_client,
    unexportable_keys::UnexportableKeyService* unexportable_key_service,
#if BUILDFLAG(IS_WIN)
        BraveMutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback
		reauth_callback,
#endif
    network::NetworkConnectionTracker* network_connection_tracker) { ... 
 
 std::make_unique<BraveMutableProfileOAuth2TokenServiceDelegate> ( ... 
#if BUILDFLAG(IS_WIN)
      reauth_callback
#else
>>> 
 MutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback() 
<<< 
#endif
 ... ) ...  } ...  } ...  
```
### patch
```cpp
      BraveMutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback()

```

### match
```cpp
...
 
 namespace { ... 
 std::unique_ptr<ProfileOAuth2TokenServiceDelegate>
CreateOAuth2TokenServiceDelegate ( ... 
>>> 
 MutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback 
<<< 
...) ...  } ...  
```
### patch
```cpp
    BraveMutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback

```

### match
```cpp
...
 
 namespace { ... 
 
 std::unique_ptr<ProfileOAuth2TokenServiceDelegate>
CreateOAuth2TokenServiceDelegate(
    AccountTrackerService* account_tracker_service,
    SigninClient* signin_client,
#if BUILDFLAG(IS_CHROMEOS)
    account_manager::AccountManagerFacade* account_manager_facade,
    bool is_regular_profile,
#endif  // BUILDFLAG(IS_CHROMEOS)
#if BUILDFLAG(ENABLE_DICE_SUPPORT)
    bool delete_signin_cookies_on_exit,
#endif  // BUILDFLAG(ENABLE_DICE_SUPPORT)
#if BUILDFLAG(ENABLE_DICE_SUPPORT)
    scoped_refptr<TokenWebData> token_web_data,
    unexportable_keys::UnexportableKeyService* unexportable_key_service,
#endif
#if BUILDFLAG(IS_IOS)
    std::unique_ptr<DeviceAccountsProvider> device_accounts_provider,
#endif
#if BUILDFLAG(IS_WIN)
        BraveMutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback
		reauth_callback,
#endif
    network::NetworkConnectionTracker* network_connection_tracker) { ... 
>>> 
 // Fall back to |MutableProfileOAuth2TokenServiceDelegate| on all platforms 
<<< 
// other than Android, iOS, and Chrome OS (Ash).
 ... } ...  } ...  
```
### patch
```cpp
  // Fall back to |BraveMutableProfileOAuth2TokenServiceDelegate| on all platforms

```

### match
```cpp
...
 std::unique_ptr<ProfileOAuth2TokenService> BuildProfileOAuth2TokenService ( ... 
>>> 
 MutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback 
<<< 
...) ...  
```
### patch
```cpp
    BraveMutableProfileOAuth2TokenServiceDelegate::FixRequestErrorCallback

```

