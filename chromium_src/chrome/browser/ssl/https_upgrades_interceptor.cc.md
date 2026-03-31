### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/browser/ssl/https_upgrades_interceptor.h"
 
 >>> 
#include "base/functional/bind.h"

 ...
```
### patch
```cpp
#include "base/feature_list.h"

```

### match
```cpp
...
#include "base/strings/string_number_conversions.h"

 #include "base/strings/stringprintf.h"
 
 >>> 
#include "build/build_config.h"

 ...
```
### patch
```cpp
#include "brave/browser/brave_browser_process.h"
#include "brave/components/brave_shields/core/browser/brave_shields_utils.h"

```

### match
```cpp
...
#include "mojo/public/cpp/bindings/remote.h"

 #include "mojo/public/cpp/system/data_pipe.h"
 
 >>> 
#include "net/base/url_util.h"

 ...
```
### patch
```cpp
#include "net/base/features.h"

```

### match
```cpp
...
 void HttpsUpgradesInterceptor::MaybeCreateLoader ( ... 
 content::URLLoaderRequestInterceptor::LoaderCallback callback 
 ) 
 { 
 >>> 
DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
 ... } ...
```
### patch
```cpp
if (base::FeatureList::IsEnabled(FLAG.name == features::kHttpsUpgrades.name
                ? net::features::kBraveHttpsByDefault
                : net::features::kBraveHttpsByDefault)) {
      HostContentSettingsMap* map =
          HostContentSettingsMapFactory::GetForProfile(browser_context);
      if (!map ||
          !brave_shields::ShouldUpgradeToHttps(
              map, tentative_resource_request.url,
              g_brave_browser_process->https_upgrade_exceptions_service())) {
        std::move(callback).Run({});
        return;
      }
      http_interstitial_enabled_by_pref_ = brave_shields::ShouldForceHttps(
          map, tentative_resource_request.url);
    }
    MaybeCreateLoader_ChromiumImpl(tentative_resource_request,
                                   browser_context, std::move(callback));
  }
  void HttpsUpgradesInterceptor::MaybeCreateLoader_ChromiumImpl(
    const network::ResourceRequest& tentative_resource_request,
    content::BrowserContext* browser_context,
    content::URLLoaderRequestInterceptor::LoaderCallback callback) {

```

### match
```cpp
...
 
 void HttpsUpgradesInterceptor::MaybeCreateLoader_ChromiumImpl(
	    const network::ResourceRequest& tentative_resource_request,
	    content::BrowserContext* browser_context,
	    content::URLLoaderRequestInterceptor::LoaderCallback callback) { ...   >>> 
 if 
 (base::FeatureList::IsEnabled(features::kHttpsFirstModeIncognito)) 
 {  <<< 
if (prefs && prefs->GetBoolean(prefs::kHttpsFirstModeIncognito) &&
        profile->IsIncognitoProfile()) {
      interstitial_state_->enabled_by_incognito = true;
    }
 ... } ...  } ...
```
### patch
```cpp
if (base::FeatureList::IsEnabled(FLAG.name == features::kHttpsUpgrades.name
                ? net::features::kBraveHttpsByDefault
                :features::kHttpsFirstModeIncognito)) {

```

### match
```cpp
...
 
 void HttpsUpgradesInterceptor::MaybeCreateLoader_ChromiumImpl(
	    const network::ResourceRequest& tentative_resource_request,
	    content::BrowserContext* browser_context,
	    content::URLLoaderRequestInterceptor::LoaderCallback callback) { ...   >>> 
 if 
 (net::IsLocalhost(tentative_resource_request.url)) 
 {  <<< 
RecordNavigationRequestSecurityLevel(
        NavigationRequestSecurityLevel::kLocalhost);
 ... } ...  } ...
```
### patch
```cpp
if (net::IsLocalhostOrOnion(tentative_resource_request.url)) {

```

### match
```cpp
...
  >>> 
 if 
 ( 
 !base::FeatureList::IsEnabled(features::kHttpsUpgrades) 
 &&  <<< ...
```
### patch
```cpp
if (!base::FeatureList::IsEnabled(FLAG.name == features::kHttpsUpgrades.name
                ? net::features::kBraveHttpsByDefault
                :features::kHttpsUpgrades) &&

```

