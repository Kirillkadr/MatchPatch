### match
```
...
#include "chrome/browser/browsing_data/chrome_browsing_data_remover_delegate_factory.h"

 #include "base/no_destructor.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```
#include "brave/browser/browsing_data/brave_browsing_data_remover_delegate.h"

```

### match
```
...
// Copyright 2017 The Chromium Authors
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.

#include "chrome/browser/browsing_data/chrome_browsing_data_remover_delegate_factory.h"

#include "base/no_destructor.h"
#include "brave/browser/browsing_data/brave_browsing_data_remover_delegate.h"
#include "build/build_config.h"
#include "chrome/browser/autofill/personal_data_manager_factory.h"
#include "chrome/browser/browsing_data/chrome_browsing_data_remover_delegate.h"
#include "chrome/browser/content_settings/host_content_settings_map_factory.h"
#include "chrome/browser/domain_reliability/service_factory.h"
#include "chrome/browser/history/history_service_factory.h"
#include "chrome/browser/history/web_history_service_factory.h"
#include "chrome/browser/password_manager/account_password_store_factory.h"
#include "chrome/browser/password_manager/profile_password_store_factory.h"
#include "chrome/browser/preloading/prefetch/no_state_prefetch/no_state_prefetch_manager_factory.h"
#include "chrome/browser/profiles/profile.h"
#include "chrome/browser/search_engines/template_url_service_factory.h"
#include "chrome/browser/sessions/tab_restore_service_factory.h"
#include "chrome/browser/webdata_services/web_data_service_factory.h"
#include "content/public/browser/browser_context.h"
#include "extensions/buildflags/buildflags.h"

#if BUILDFLAG(ENABLE_EXTENSIONS)
#include "chrome/browser/extensions/activity_log/activity_log.h"
#include "extensions/browser/extension_prefs_factory.h"
#endif

#if BUILDFLAG(ENABLE_SESSION_SERVICE)
#include "chrome/browser/sessions/session_service_factory.h"
#endif

#if BUILDFLAG(IS_ANDROID)
#include "chrome/browser/feed/feed_service_factory.h"
#include "components/feed/feed_feature_list.h"
#endif  // BUILDFLAG(IS_ANDROID

// static
ChromeBrowsingDataRemoverDelegateFactory*
ChromeBrowsingDataRemoverDelegateFactory::GetInstance() {
  static base::NoDestructor<ChromeBrowsingDataRemoverDelegateFactory> instance;
  return instance.get();
}

// static
  >>> 
 ChromeBrowsingDataRemoverDelegate 
 *  <<< ... ) ...  
```
### patch
```
BraveBrowsingDataRemoverDelegate*

```

### match
```
...
 BraveBrowsingDataRemoverDelegate*
ChromeBrowsingDataRemoverDelegateFactory::GetForProfile(Profile* profile) { ...   >>> 
 return 
 static_cast<ChromeBrowsingDataRemoverDelegate*> 
 (  <<< ... 
GetInstance()->GetServiceForBrowserContext(profile, true)
 ... ) ...  } ...  
```
### patch
```
  return static_cast<BraveBrowsingDataRemoverDelegate*>(

```

### match
```
...
 std::unique_ptr<KeyedService>
ChromeBrowsingDataRemoverDelegateFactory::BuildServiceInstanceForBrowserContext(
    content::BrowserContext* context) const { ... 
DCHECK(!profile->IsGuestSession() || profile->IsOffTheRecord());  >>> 
 return std::make_unique<ChromeBrowsingDataRemoverDelegate>(context);  <<< ... } ...  
```
### patch
```
  return std::make_unique<BraveBrowsingDataRemoverDelegate>(context);

```

