### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/content_settings/browser/content_settings_manager_impl.h"

 ... 
```
### patch
```cpp
#include "components/content_settings/browser/content_settings_manager_impl.h"

```

### match
```cpp
...
#include "components/content_settings/browser/content_settings_manager_impl.h"

 #include "components/content_settings/browser/content_settings_manager_impl.h"
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```cpp
#include <optional>

```

### match
```cpp
...
 
 namespace content_settings { ... 
 
 void ContentSettingsManagerImpl::CreateOnThread(
    int render_process_id,
    mojo::PendingReceiver<content_settings::mojom::ContentSettingsManager>
        receiver,
    scoped_refptr<CookieSettings> cookie_settings,
    std::unique_ptr<Delegate> delegate) { ... 
mojo::MakeSelfOwnedReceiver(
      base::WrapUnique(new ContentSettingsManagerImpl(
          render_process_id, std::move(delegate), cookie_settings)),
      std::move(receiver));
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void ContentSettingsManagerImpl::AllowEphemeralStorageAccess(
    const blink::LocalFrameToken& frame_token,
    const url::Origin& origin,
    const net::SiteForCookies& site_for_cookies,
    const url::Origin& top_frame_origin,
    AllowEphemeralStorageAccessCallback callback) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  url::Origin storage_origin;
  const bool should_use = cookie_settings_->ShouldUseEphemeralStorage(
      origin, site_for_cookies, top_frame_origin, storage_origin);
  std::move(callback).Run(should_use
                              ? std::make_optional<url::Origin>(storage_origin)
                              : std::nullopt);
}

void ContentSettingsManagerImpl::GetBraveShieldsSettings(
    const blink::LocalFrameToken& frame_token,
    GetBraveShieldsSettingsCallback callback) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  delegate_->GetBraveShieldsSettings(
      content::GlobalRenderFrameHostToken(render_process_id_, frame_token),
      std::move(callback));
}

```

