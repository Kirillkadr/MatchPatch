### match
```
...
>>>
 WebWindowFeatures 
 GetWindowFeaturesFromString 
 ( 
 const String& feature_string 
 ,  <<< ... 
LocalDOMWindow* dom_window
 ... ) ...  
```
### patch
```
WebWindowFeatures GetWindowFeaturesFromString(const blink::String& feature_string, 
                              LocalDOMWindow* dom_window) {
    return MaybeFarbleWindowFeatures(feature_string, dom_window);
  }
  WebWindowFeatures GetWindowFeaturesFromString_ChromiumImpl(const String& feature_string,

```

### match
```
...
 namespace blink { ... 
Frame* CreateNewWindow(LocalFrame& opener_frame,
                       FrameLoadRequest& request,
                       const AtomicString& frame_name) {
  LocalDOMWindow& opener_window = *opener_frame.DomWindow();
  DCHECK(request.GetResourceRequest().RequestorOrigin() ||
         opener_window.Url().IsEmpty());
  DCHECK_EQ(kNavigationPolicyCurrentTab, request.GetNavigationPolicy());

  if (opener_window.document()->PageDismissalEventBeingDispatched() !=
      Document::kNoDismissal) {
    return nullptr;
  }

  request.SetFrameType(mojom::RequestContextFrameType::kAuxiliary);

  const KURL& url = request.GetResourceRequest().Url();
  if (url.ProtocolIsJavaScript()) {
    if (opener_window
            .CheckAndGetJavascriptUrl(request.JavascriptWorld(), url,
                                      nullptr /* element */)
            .empty()) {
      return nullptr;
    }
  }

  if (!opener_window.GetSecurityOrigin()->CanDisplay(url)) {
    opener_window.AddConsoleMessage(MakeGarbageCollected<ConsoleMessage>(
        mojom::blink::ConsoleMessageSource::kSecurity,
        mojom::blink::ConsoleMessageLevel::kError,
        StrCat({"Not allowed to load local resource: ", url.ElidedString()})));
    return nullptr;
  }

  request.SetInitiatorFrameToken(opener_frame.GetLocalFrameToken());
  request.SetInitiatorNavigationStateKeepAliveHandle(
      opener_frame.IssueKeepAliveHandle());

  // Make a copy in order to adjust the requested size. We don't constrain the
  // geometry to the screen (via ChromeClientImpl::AdjustWindowRectForDisplay)
  // because the browser may honor cross-screen bounds.
  WebWindowFeatures features(request.GetWindowFeatures());
  const auto& picture_in_picture_window_options =
      request.GetPictureInPictureWindowOptions();
  if (picture_in_picture_window_options.has_value()) {
    request.SetNavigationPolicy(kNavigationPolicyPictureInPicture);
  } else {
    request.SetNavigationPolicy(NavigationPolicyForCreateWindow(features));
    probe::WindowOpen(&opener_window, url, frame_name, features,
                      LocalFrame::HasTransientUserActivation(&opener_frame));
  }

  int min_size = kMinimumWindowSize;
  // The minimum size from popups opened from borderless apps differs from
  // normal apps. When window.open is called, display-mode for the new frame is
  // still undefined as the app hasn't loaded yet, thus opener frame is used.
  bool new_popup = request.GetNavigationPolicy() ==
                   NavigationPolicy::kNavigationPolicyNewPopup;
  bool borderless = false;
  if (auto* widget = opener_frame.GetWidgetForLocalRoot()) {
    borderless = widget->DisplayMode() == mojom::blink::DisplayMode::kUnframed;
  }
  if (new_popup && borderless) {
    min_size = kMinimumBorderlessWindowSize;
  }
  if (features.width) {
    features.width = std::max(features.width, min_size);
  }
  if (features.height) {
    features.height = std::max(features.height, min_size);
  }

  // Sandboxed frames cannot open new auxiliary browsing contexts.
  if (opener_window.IsSandboxed(
          network::mojom::blink::WebSandboxFlags::kPopups)) {
    // FIXME: This message should be moved off the console once a solution to
    // https://bugs.webkit.org/show_bug.cgi?id=103274 exists.
    opener_window.AddConsoleMessage(MakeGarbageCollected<ConsoleMessage>(
        mojom::blink::ConsoleMessageSource::kSecurity,
        mojom::blink::ConsoleMessageLevel::kError,
        StrCat({"Blocked opening '", url.ElidedString(),
                "' in a new window because the request was made in a sandboxed "
                "frame whose 'allow-popups' permission is not set."})));
    return nullptr;
  }

  network::mojom::blink::WebSandboxFlags sandbox_flags =
      opener_window.IsSandboxed(network::mojom::blink::WebSandboxFlags::
                                    kPropagatesToAuxiliaryBrowsingContexts)
          ? opener_window.GetSandboxFlags()
          : network::mojom::blink::WebSandboxFlags::kNone;

  SessionStorageNamespaceId new_namespace_id =
      AllocateSessionStorageNamespaceId();

  Page* old_page = opener_frame.GetPage();
  if (!features.noopener) {
    CoreInitializer::GetInstance().CloneSessionStorage(old_page,
                                                       new_namespace_id);
  }

  bool consumed_user_gesture = false;
  Page* page = old_page->GetChromeClient().CreateWindow(
      &opener_frame, request, frame_name, features, sandbox_flags,
      new_namespace_id, consumed_user_gesture);
  if (!page)
    return nullptr;

  if (page == old_page) {
    Frame* frame = &opener_frame.Tree().Top();
    if (!opener_frame.CanNavigate(*frame))
      return nullptr;
    if (!features.noopener)
      frame->SetOpener(&opener_frame);
    return frame;
  }

  DCHECK(page->MainFrame());
  LocalFrame& frame = *To<LocalFrame>(page->MainFrame());

  page->SetWindowFeatures(features);

  frame.View()->SetCanHaveScrollbars(!features.is_popup);

  // GetWebView() may return nullptr in tests
  if (auto* web_view = page->GetChromeClient().GetWebView()) {
    if (auto* dev_tools_agent = web_view->MainFrameImpl()->DevToolsAgentImpl(
            /*create_if_necessary=*/false)) {
      dev_tools_agent->DidShowNewWindow();
    }
  }

  MaybeLogWindowOpen(opener_frame);
  return &frame;
}
 } 
 // namespace blink 
 >>> 
 ... 
```
### patch
```
namespace {

blink::WebWindowFeatures MaybeFarbleWindowFeatures(
    const blink::String& feature_string,
    blink::LocalDOMWindow* dom_window) {
  blink::WebWindowFeatures window_features =
      GetWindowFeaturesFromString_ChromiumImpl(feature_string, dom_window);
  blink::ExecutionContext* context = dom_window->GetExecutionContext();
  if (brave::BlockScreenFingerprinting(context)) {
    if (window_features.x_set) {
      window_features.x += dom_window->screenX_ChromiumImpl();
    }
    if (window_features.y_set) {
      window_features.y += dom_window->screenY_ChromiumImpl();
    }
    if (window_features.width_set) {
      int max_width = dom_window->screen()->width();
      if (window_features.width > max_width) {
        window_features.width = max_width;
      }
    }
    if (window_features.height_set) {
      int max_height = dom_window->screen()->height();
      if (window_features.height > max_height) {
        window_features.height = max_height;
      }
    }
  }
  return window_features;
}

}  // namespace
```

