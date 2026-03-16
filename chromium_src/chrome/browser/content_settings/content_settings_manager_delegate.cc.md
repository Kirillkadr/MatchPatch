### match
```
...
#include "base/feature_list.h"

 #include "base/task/sequenced_task_runner.h"
 
 >>> 
#include "chrome/browser/content_settings/cookie_settings_factory.h"

 ... 
```
### patch
```
#include "brave/browser/brave_shields/brave_shields_settings_service_factory.h"
#include "brave/components/brave_shields/core/browser/brave_shields_settings_service.h"
#include "brave/components/brave_shields/core/browser/brave_shields_utils.h"
#include "brave/components/brave_shields/core/common/shields_settings.mojom-shared.h"

```

### match
```
...
#include "brave/components/brave_shields/core/common/shields_settings.mojom-shared.h"

 #include "chrome/browser/content_settings/cookie_settings_factory.h"
 
 >>> 
#include "chrome/browser/profiles/profile.h"

 ... 
```
### patch
```
#include "chrome/browser/content_settings/host_content_settings_map_factory.h"

```

### match
```
...
#include "components/content_settings/browser/page_specific_content_settings.h"

 #include "components/content_settings/core/browser/cookie_settings.h"
 
 >>> 
#include "content/public/browser/browser_task_traits.h"

 ... 
```
### patch
```
#include "components/user_prefs/user_prefs.h"

```

### match
```
...
 namespace { ... 
void PostTaskOnSequence(scoped_refptr<base::SequencedTaskRunner> task_runner,
                        base::OnceCallback<void(bool)> callback,
                        bool result) {
  task_runner->PostTask(FROM_HERE, base::BindOnce(std::move(callback), result));
}
 #endif 
 >>> 
 ... } ...  
```
### patch
```
bool IsJsBlockingEnforced(content::BrowserContext* browser_context,
                          const GURL& url) {
  Profile* profile = Profile::FromBrowserContext(browser_context);
  auto* settings_service =
      BraveShieldsSettingsServiceFactory::GetForProfile(profile);
  if (!settings_service) {
    return false;
  }

  return settings_service->IsJsBlockingEnforced(url);
}

brave_shields::mojom::ShieldsSettingsPtr GetBraveShieldsSettingsOnUI(
    const content::GlobalRenderFrameHostToken& frame_token) {
  content::RenderFrameHost* rfh =
      content::RenderFrameHost::FromFrameToken(frame_token);
  if (!rfh) {
    return brave_shields::mojom::ShieldsSettings::New();
  }
  content::RenderFrameHost* top_frame_rfh = rfh->GetOutermostMainFrame();
  if (!top_frame_rfh) {
    return brave_shields::mojom::ShieldsSettings::New();
  }

  const GURL& top_frame_url = top_frame_rfh->GetLastCommittedURL();

  content::BrowserContext* browser_context = rfh->GetBrowserContext();
  const brave_shields::mojom::FarblingLevel farbling_level =
      brave_shields::GetFarblingLevel(
          HostContentSettingsMapFactory::GetForProfile(browser_context),
          top_frame_url);
  const base::Token farbling_token =
      farbling_level != brave_shields::mojom::FarblingLevel::OFF
          ? brave_shields::GetFarblingToken(
                HostContentSettingsMapFactory::GetForProfile(browser_context),
                top_frame_url)
          : base::Token();
  PrefService* pref_service = user_prefs::UserPrefs::Get(browser_context);

  return brave_shields::mojom::ShieldsSettings::New(
      farbling_level, farbling_token, std::vector<std::string>(),
      brave_shields::IsReduceLanguageEnabledForProfile(pref_service),
      IsJsBlockingEnforced(browser_context, top_frame_url));
}


```

### match
```
...
 std::unique_ptr<content_settings::ContentSettingsManagerImpl::Delegate>
ContentSettingsManagerDelegate::Clone() { ... 
return std::make_unique<ContentSettingsManagerDelegate>();
 } 
 >>> 
 ... 
```
### patch
```

void ContentSettingsManagerDelegate::GetBraveShieldsSettings(
    const content::GlobalRenderFrameHostToken& frame_token,
    content_settings::mojom::ContentSettingsManager::
        GetBraveShieldsSettingsCallback callback) {
  content::GetUIThreadTaskRunner({})->PostTaskAndReplyWithResult(
      FROM_HERE, base::BindOnce(&GetBraveShieldsSettingsOnUI, frame_token),
      std::move(callback));
}

```

