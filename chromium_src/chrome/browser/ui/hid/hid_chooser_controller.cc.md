### match
```cpp
...
#include "base/functional/bind.h"

 #include "base/strings/stringprintf.h"
 
 >>> 
#include "chrome/browser/chooser_controller/title_util.h"

 ... 
```
### patch
```cpp
#include "brave/components/brave_wallet/common/buildflags/buildflags.h"

```

### match
```cpp
...
#include "chrome/common/url_constants.h"

 #include "chrome/grit/generated_resources.h"
 
 >>> 
#include "components/strings/grit/components_strings.h"

 ... 
```
### patch
```cpp
#include "components/grit/brave_components_strings.h"

```

### match
```cpp
...
#include "services/device/public/cpp/hid/hid_switches.h"

 #include "ui/base/l10n/l10n_util.h"
 
 >>> 
namespace {

std::string PhysicalDeviceIdFromDeviceInfo(
    const device::mojom::HidDeviceInfo& device) {
  // A single physical device may expose multiple HID interfaces, each
  // represented by a HidDeviceInfo object. When a device exposes multiple
  // HID interfaces, the HidDeviceInfo objects will share a common
  // |physical_device_id|. Group these devices so that a single chooser item
  // is shown for each physical device. If a device's physical device ID is
  // empty, use its GUID instead.
  return device.physical_device_id.empty() ? device.guid
                                           : device.physical_device_id;
}

bool FilterMatch(const blink::mojom::HidDeviceFilterPtr& filter,
                 const device::mojom::HidDeviceInfo& device) {
  if (filter->device_ids) {
    if (filter->device_ids->is_vendor()) {
      if (filter->device_ids->get_vendor() != device.vendor_id) {
        return false;
      }
    } else if (filter->device_ids->is_vendor_and_product()) {
      const auto& vendor_and_product =
          filter->device_ids->get_vendor_and_product();
      if (vendor_and_product->vendor != device.vendor_id) {
        return false;
      }
      if (vendor_and_product->product != device.product_id) {
        return false;
      }
    }
  }

  if (filter->usage) {
    if (filter->usage->is_page()) {
      if (!std::ranges::contains(
              device.collections, filter->usage->get_page(),
              [](const device::mojom::HidCollectionInfoPtr& c) {
                return c->usage->usage_page;
              })) {
        return false;
      }
    } else if (filter->usage->is_usage_and_page()) {
      const auto& usage_and_page = filter->usage->get_usage_and_page();
      if (std::ranges::none_of(
              device.collections,
              [&usage_and_page](const device::mojom::HidCollectionInfoPtr& c) {
                return usage_and_page->usage_page == c->usage->usage_page &&
                       usage_and_page->usage == c->usage->usage;
              })) {
        return false;
      }
    }
  }
  return true;
}

}
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
#include "brave/components/brave_wallet/browser/brave_wallet_utils.h"
#endif


```

### match
```cpp
...
 namespace 
 { 
 >>> 
std::string PhysicalDeviceIdFromDeviceInfo(
    const device::mojom::HidDeviceInfo& device) {
  // A single physical device may expose multiple HID interfaces, each
  // represented by a HidDeviceInfo object. When a device exposes multiple
  // HID interfaces, the HidDeviceInfo objects will share a common
  // |physical_device_id|. Group these devices so that a single chooser item
  // is shown for each physical device. If a device's physical device ID is
  // empty, use its GUID instead.
  return device.physical_device_id.empty() ? device.guid
                                           : device.physical_device_id;
}
 ... } ...  
```
### patch
```cpp
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
std::u16string BraveCreateTitleLabel() {
  auto wallet_title = l10n_util::GetStringUTF16(IDS_BRAVE_WALLET);
  return l10n_util::GetStringFUTF16(IDS_HID_CHOOSER_PROMPT, wallet_title);
}
#endif


```

### match
```cpp
...
 
 namespace { ... 
bool FilterMatch(const blink::mojom::HidDeviceFilterPtr& filter,
                 const device::mojom::HidDeviceInfo& device) {
  if (filter->device_ids) {
    if (filter->device_ids->is_vendor()) {
      if (filter->device_ids->get_vendor() != device.vendor_id) {
        return false;
      }
    } else if (filter->device_ids->is_vendor_and_product()) {
      const auto& vendor_and_product =
          filter->device_ids->get_vendor_and_product();
      if (vendor_and_product->vendor != device.vendor_id) {
        return false;
      }
      if (vendor_and_product->product != device.product_id) {
        return false;
      }
    }
  }

  if (filter->usage) {
    if (filter->usage->is_page()) {
      if (!std::ranges::contains(
              device.collections, filter->usage->get_page(),
              [](const device::mojom::HidCollectionInfoPtr& c) {
                return c->usage->usage_page;
              })) {
        return false;
      }
    } else if (filter->usage->is_usage_and_page()) {
      const auto& usage_and_page = filter->usage->get_usage_and_page();
      if (std::ranges::none_of(
              device.collections,
              [&usage_and_page](const device::mojom::HidCollectionInfoPtr& c) {
                return usage_and_page->usage_page == c->usage->usage_page &&
                       usage_and_page->usage == c->usage->usage;
              })) {
        return false;
      }
    }
  }
  return true;
}
 } 
 // namespace 
 >>> 
HidChooserController::HidChooserController(
    content::RenderFrameHost* render_frame_host,
    std::vector<blink::mojom::HidDeviceFilterPtr> filters,
    std::vector<blink::mojom::HidDeviceFilterPtr> exclusion_filters,
    content::HidChooser::Callback callback)
    : ChooserController(
          CreateChooserTitle(render_frame_host, IDS_HID_CHOOSER_PROMPT)),
      filters_(std::move(filters)),
      exclusion_filters_(std::move(exclusion_filters)),
      callback_(std::move(callback)),
      initiator_document_(render_frame_host->GetWeakDocumentPtr()),
      origin_(render_frame_host->GetMainFrame()->GetLastCommittedOrigin()) {
  // The use above of GetMainFrame is safe as content::HidService instances are
  // not created for fenced frames.
  DCHECK(!render_frame_host->IsNestedWithinFencedFrame());

  auto* web_contents =
      content::WebContents::FromRenderFrameHost(render_frame_host);
  auto* profile =
      Profile::FromBrowserContext(web_contents->GetBrowserContext());
  chooser_context_ =
      HidChooserContextFactory::GetForProfile(profile)->AsWeakPtr();
  DCHECK(chooser_context_);

  chooser_context_->GetHidManager()->GetDevices(base::BindOnce(
      &HidChooserController::OnGotDevices, weak_factory_.GetWeakPtr()));
}
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
#define CreateChooserTitle                                                  \
  brave_wallet::IsBraveWalletOrigin(                                        \
      render_frame_host->GetOutermostMainFrame()->GetLastCommittedOrigin()) \
      ? BraveCreateTitleLabel()                                             \
      : CreateChooserTitle
#endif


```

### match
```cpp
...
 
 void HidChooserController::UpdateDeviceInfo(
    const device::mojom::HidDeviceInfo& device) { ... 
*device_it = device.Clone();
 } 
 >>> 
 ... 
```
### patch
```cpp

#undef CreateChooserTitle
#endif
```

