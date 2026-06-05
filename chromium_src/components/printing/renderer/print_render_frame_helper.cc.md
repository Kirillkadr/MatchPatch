/* Copyright (c) 2024 The Brave Authors. All rights reserved.
 * This Source Code Form is subject to the terms of the Mozilla Public
 * License, v. 2.0. If a copy of the MPL was not distributed with this file,
 * You can obtain one at https://mozilla.org/MPL/2.0/. */

#include "components/printing/renderer/print_render_frame_helper.h"

#define PrintRenderFrameHelper PrintRenderFrameHelper_ChromiumImpl
#include <components/printing/renderer/print_render_frame_helper.cc>
#undef PrintRenderFrameHelper

namespace printing {

PrintRenderFrameHelper::PrintRenderFrameHelper(
    content::RenderFrame* render_frame,
    std::unique_ptr<Delegate> delegate)
    : PrintRenderFrameHelper_ChromiumImpl(render_frame, std::move(delegate)) {}
### match
```cpp
...
 
 namespace permissions { ... 
 
 namespace { ... 
 
 int GetIconIdAndroid(RequestType type) { ... 
 
 case RequestType : ... 
 return IDR_ANDROID_INFOBAR_WINDOW_MANAGEMENT; 
 >>> 
 ... } ...  } ...  } ...  
```
### patch
```cpp
    case RequestType::kWidevine:
    case RequestType::kBraveEthereum:
    case RequestType::kBraveSolana:
    case RequestType::kBraveCardano:
    case RequestType::kBraveGoogleSignInPermission:
    case RequestType::kBraveOpenAIChat:
      return IDR_ANDROID_INFOBAR_PERMISSION_COOKIE;

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 std::optional<RequestType> ContentSettingsTypeToRequestTypeIfExists(
    ContentSettingsType content_settings_type) { ... 
 
 case ContentSettingsType : ... 
 return RequestType::kIdentityProvider; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
      #if BUILDFLAG(ENABLE_BRAVE_WALLET)
    case ContentSettingsType::BRAVE_ETHEREUM:
      return RequestType::kBraveEthereum;
    case ContentSettingsType::BRAVE_SOLANA:
      return RequestType::kBraveSolana;
    case ContentSettingsType::BRAVE_CARDANO:
      return RequestType::kBraveCardano;
+#endif
    case ContentSettingsType::BRAVE_GOOGLE_SIGN_IN:
      return RequestType::kBraveGoogleSignInPermission;
    case ContentSettingsType::BRAVE_OPEN_AI_CHAT:
      return RequestType::kBraveOpenAIChat;
    case ContentSettingsType::DEFAULT:
      return RequestType::kWidevine;

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 std::optional<ContentSettingsType> RequestTypeToContentSettingsType(
    RequestType request_type) { ... 
 
 switch (request_type) { ... 
case RequestType::kWebAppInstallation:
      return ContentSettingsType::WEB_APP_INSTALLATION;
 #endif 
 // !BUILDFLAG(IS_ANDROID) && !BUILDFLAG(IS_IOS) 
 >>> 
// Not associated with a ContentSettingsType.
 ... } ...  } ...  } ...  
```
### patch
```cpp
case RequestType::kBraveGoogleSignInPermission:
      return ContentSettingsType::BRAVE_GOOGLE_SIGN_IN;
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
    case RequestType::kBraveEthereum:
      return ContentSettingsType::BRAVE_ETHEREUM;
    case RequestType::kBraveSolana:
      return ContentSettingsType::BRAVE_SOLANA;
    case RequestType::kBraveCardano:
     return ContentSettingsType::BRAVE_CARDANO;
#endif
    case RequestType::kBraveOpenAIChat:
      return ContentSettingsType::BRAVE_OPEN_AI_CHAT;

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 const char* PermissionKeyForRequestType(permissions::RequestType request_type) { ... 
 
 case permissions : ... 
 return "identity_provider"; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
      case permissions::RequestType::kWidevine:
      return "widevine";
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
    case permissions::RequestType::kBraveEthereum:
      return "brave_ethereum";
    case permissions::RequestType::kBraveSolana:
      return "brave_solana";
    case permissions::RequestType::kBraveCardano:
      return "brave_cardano";
#else
    case permissions::RequestType::kBraveEthereum:
    case permissions::RequestType::kBraveSolana:
    case permissions::RequestType::kBraveCardano:
      NOTREACHED();
#endif
    case permissions::RequestType::kBraveGoogleSignInPermission:
      return "brave_google_sign_in";
    case permissions::RequestType::kBraveOpenAIChat:
      return "brave_ai_chat";

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 const char* PermissionKeyForRequestType(permissions::RequestType request_type) { ... 
return nullptr;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
RequestType ContentSettingsTypeToRequestType(
    ContentSettingsType content_settings_type) {
  switch (content_settings_type) {
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
    case ContentSettingsType::BRAVE_ETHEREUM:
      return RequestType::kBraveEthereum;
    case ContentSettingsType::BRAVE_SOLANA:
      return RequestType::kBraveSolana;
    case ContentSettingsType::BRAVE_CARDANO:
      return RequestType::kBraveCardano;
#endif
    case ContentSettingsType::BRAVE_GOOGLE_SIGN_IN:
      return RequestType::kBraveGoogleSignInPermission;
    case ContentSettingsType::BRAVE_OPEN_AI_CHAT:
      return RequestType::kBraveOpenAIChat;
    case ContentSettingsType::DEFAULT:
      // Currently we have only one DEFAULT type that is
      // not mapped, which is Widevine, it's used for
      // UMA purpose only
      return RequestType::kWidevine;
    default:
      return ContentSettingsTypeToRequestType_ChromiumImpl(
          content_settings_type);
  }
}
std::optional<ContentSettingsType> RequestTypeToContentSettingsType(
    RequestType request_type) {
  switch (request_type) {
    case RequestType::kBraveGoogleSignInPermission:
      return ContentSettingsType::BRAVE_GOOGLE_SIGN_IN;
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
    case RequestType::kBraveEthereum:
      return ContentSettingsType::BRAVE_ETHEREUM;
    case RequestType::kBraveSolana:
      return ContentSettingsType::BRAVE_SOLANA;
    case RequestType::kBraveCardano:
      return ContentSettingsType::BRAVE_CARDANO;
#endif
    case RequestType::kBraveOpenAIChat:
      return ContentSettingsType::BRAVE_OPEN_AI_CHAT;
    default:
      return RequestTypeToContentSettingsType_ChromiumImpl(request_type);
  }
}

bool IsRequestablePermissionType(ContentSettingsType content_settings_type) {
  switch (content_settings_type) {
    case ContentSettingsType::BRAVE_GOOGLE_SIGN_IN:
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
    case ContentSettingsType::BRAVE_ETHEREUM:
    case ContentSettingsType::BRAVE_SOLANA:
    case ContentSettingsType::BRAVE_CARDANO:
#endif
    case ContentSettingsType::BRAVE_OPEN_AI_CHAT:
      return true;
    default:
      return IsRequestablePermissionType_ChromiumImpl(content_settings_type);
  }
}

```


PrintRenderFrameHelper::~PrintRenderFrameHelper() = default;

#if BUILDFLAG(ENABLE_PRINT_PREVIEW)
void PrintRenderFrameHelper::SetPrintPreviewUI(
    mojo::PendingAssociatedRemote<mojom::PrintPreviewUI> preview) {
  preview_ui_.reset();
  PrintRenderFrameHelper_ChromiumImpl::SetPrintPreviewUI(std::move(preview));
}

void PrintRenderFrameHelper::InitiatePrintPreview(
    bool has_selection) {
  if (!is_print_preview_extraction_) {
    PrintRenderFrameHelper_ChromiumImpl::InitiatePrintPreview(has_selection);
    return;
  }

  ScopedIPC scoped_ipc(weak_ptr_factory_.GetWeakPtr());
  if (ipc_nesting_level_ > kAllowedIpcDepthForPrint) {
    return;
  }

  if (print_in_progress_) {
    return;
  }

  blink::WebLocalFrame* frame = render_frame()->GetWebFrame();

  // If we are printing a frame with an internal PDF plugin element, find the
  // plugin node and print that instead.
  auto plugin = delegate_->GetPdfElement(frame);
  if (!plugin.IsNull()) {
    print_preview_context_.InitWithNode(plugin);
  } else {
    print_preview_context_.InitWithFrame(frame);
    print_preview_context_.DispatchBeforePrintEvent(
        weak_ptr_factory_.GetWeakPtr());
  }
  // Print Preview resets `print_in_progress_` when the dialog closes.
}

void PrintRenderFrameHelper::SetIsPrintPreviewExtraction(bool value) {
  is_print_preview_extraction_ = value;
}
#endif  // BUILDFLAG(ENABLE_PRINT_PREVIEW)

}  // namespace printing
