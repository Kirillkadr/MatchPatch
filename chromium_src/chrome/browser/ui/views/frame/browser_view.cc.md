### match
```cpp
...
 #include "base/trace_event/trace_event.h"
 
 >>> 
 ...
```
### patch
```cppч
#include "brave/browser/ui/views/brave_tab_search_bubble_host.h"
#include "brave/browser/ui/views/frame/brave_browser_view_layout.h"
#include "brave/browser/ui/views/frame/brave_tab_strip_region_view.h"
#include "brave/browser/ui/views/frame/split_view/brave_multi_contents_view.h"
#include "brave/browser/ui/views/frame/split_view/brave_multi_contents_view_delegate_impl.h"
#include "brave/browser/ui/views/infobars/brave_infobar_container_view.h"
#include "brave/browser/ui/views/side_panel/brave_side_panel_coordinator.h"
#include "brave/browser/ui/views/side_panel/side_panel.h"
#include "brave/browser/ui/views/tabs/vertical_tab_utils.h"
#include "brave/browser/ui/views/toolbar/brave_toolbar_view.h"
#include "brave/components/constants/pref_names.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/views/frame/layout/browser_view_layout.h"
 
 >>> 
 ...
```
### patch
```cpp
#include "chrome/browser/ui/views/frame/layout/browser_view_layout_impl_old.h"

```

### match
```cpp
...
  DCHECK(point); 
 >>>
```
### patch
```cpp
if (dst->GetWidget() != src->GetWidget()) {
    return false;
  }

```

### match
```cpp
...
 
 class BrowserView::ExclusiveAccessContextImpl
    : public ExclusiveAccessContext,
      public ExclusiveAccessBubbleViewsContext { ... 
 void 
 UpdateExclusiveAccessBubble 
 ( 
 >>> 
 ... ) ...  } ...  
```
### patch
```cpp
      const ExclusiveAccessBubbleParams& params,
      ExclusiveAccessBubbleHideCallback first_hide_callback)  override;
  virtual void UpdateExclusiveAccessBubble_ChromiumImpl(

```

### match
```cpp
...
 
 BrowserView::BrowserView(Browser* browser)
    : views::ClientView(nullptr, nullptr),
      exclusive_access_context_(
          std::make_unique<ExclusiveAccessContextImpl>(*this)),
      browser_(browser) { ... 
>>> 
 auto multi_contents_view = std::make_unique<MultiContentsView>(
      this, std::make_unique<MultiContentsViewDelegateImpl>(*browser_)); 
<<< 
...} ...  
```
### patch
```cpp
  auto multi_contents_view = std::make_unique<BraveMultiContentsView>(
      this, std::make_unique<BraveMultiContentsViewDelegateImpl>(*browser_));

```

### match
```cpp
...
 
 BrowserView::BrowserView(Browser* browser)
    : views::ClientView(nullptr, nullptr),
      exclusive_access_context_(
          std::make_unique<ExclusiveAccessContextImpl>(*this)),
      browser_(browser) { ... 
 
 top_container_->AddChildView ( ... 
>>> 
 std::make_unique<ToolbarView>(browser_.get(), this) 
 ) 
 ; 
<<< 
...} ...  
```
### patch
```cpp
      std::make_unique<BraveToolbarView>(browser_.get(), this));

```

### match
```cpp
...
 
 BrowserView::BrowserView(Browser* browser)
    : views::ClientView(nullptr, nullptr),
      exclusive_access_context_(
          std::make_unique<ExclusiveAccessContextImpl>(*this)),
      browser_(browser) { ... 
>>> 
 AddChildView(std::make_unique<InfoBarContainerView>(this)) 
 ; 
<<< 
...} ...  
```
### patch
```cpp
      AddChildView(std::make_unique<BraveInfoBarContainerView>(this));

```

### match
```cpp
...
 
 BrowserView::BrowserView(Browser* browser)
    : views::ClientView(nullptr, nullptr),
      exclusive_access_context_(
          std::make_unique<ExclusiveAccessContextImpl>(*this)),
      browser_(browser) { ... 
>>> 
 AddChildView(std::make_unique<HorizontalTabStripRegionView>(this)) 
 ; 
<<< 
...} ...  
```
### patch
```cpp
      AddChildView(std::make_unique<BraveHorizontalTabStripRegionView>(this));

```

### match
```cpp
...
 
 void BrowserView::OnActiveTabChanged(content::WebContents* old_contents,
                                     content::WebContents* new_contents,
                                     int index,
                                     int reason) { ... 
 #endif 
 >>> 
 ... } ...  
```
### patch
```cpp
if (multi_contents_view_) {
    change_tab_contents &= !IsWebPanelContents(new_contents);
    BraveMultiContentsView::From(multi_contents_view_)
        ->set_web_panel_active(IsWebPanelContents(new_contents));
    if (IsWebPanelContents(old_contents)) {
      active_contents_view = GetActiveContentsWebView();
    }
  }

```

### match
```cpp
...
 
 WebContentsModalDialogHost* BrowserView::GetWebContentsModalDialogHost() { ... 
>>> 
 return GetBrowserViewLayout()->GetWebContentsModalDialogHost(); 
<<< 
...} ...  
```
### patch
```cpp
  return BraveBrowserViewLayout()->GetWebContentsModalDialogHost();

```

### match
```cpp
...
>>>
 BookmarkBarView 
 * BrowserView::GetBookmarkBarView() const 
 { 
 return bookmark_bar_view_.get(); 
<<< 
...} ...  
```
### patch
```cpp
BraveBookmarkBarView* BrowserView::GetBookmarkBarView() const {
  return bookmark_bar_viewx_.get();

```

### match
```cpp
...
 
 void BrowserView::MaybeUpdateStoredFocusForWebContents(
    content::WebContents* web_contents) { ... 
>>> 
 const 
 MultiContentsView::FocusableViewMap 
 * view_map 
 = 
<<< 
...} ...  
```
### patch
```cpp
  const BraveMultiContentsView::FocusableViewMap* view_map =

```

### match
```cpp
...
>>>
 SetLayoutManager 
 ( 
 BrowserViewLayout::CreateLayout 
 ( 
<<< 
...) ...  ) ...  
```
### patch
```cpp
  SetLayoutManager(BraveBrowserViewLayout::CreateLayout(

```

### match
```cpp
...
>>>
 BrowserViewLayout 
 * BrowserView::GetBrowserViewLayout() const 
 { 
 return static_cast<BrowserViewLayout*>(GetLayoutManager()); 
<<< 
...} ...  
```
### patch
```cpp
BraveBrowserViewLayout* BrowserView::GetBrowserViewLayout() const {
  return static_cast<BraveBrowserViewLayout*>(GetLayoutManager());

```

### match
```cpp
...
 
 bool BrowserView::MaybeShowBookmarkBar(WebContents* contents) { ... 
 
 if (!bookmark_bar_view_) { ... 
>>> 
 std::make_unique<BookmarkBarView>(browser_.get(), this) 
 ; 
<<< 
...} ...  } ...  
```
### patch
```cpp
        std::make_unique<BraveBookmarkBarView>(browser_.get(), this);

```

### match
```cpp
...
 #endif 
 // BUILDFLAG(ENTERPRISE_SCREENSHOT_PROTECTION) 
 >>> 
 ... 
```
### patch
```cpp
bool BrowserView::IsWebPanelContents(content::WebContents* contents) {
  NOTREACHED();
}

void BrowserView::SetNativeWindowPropertyForWidget(views::Widget* widget) {
  // Sets a kBrowserWindowKey to given child |widget| so that we can get
  // BrowserView from the |widget|.
  DCHECK(GetWidget());
  DCHECK_EQ(GetWidget(), widget->GetTopLevelWidget())
      << "The |widget| should be child of BrowserView's widget.";

  widget->SetNativeWindowProperty(kBrowserViewKey, this);
}

void BrowserView::ExclusiveAccessContextImpl::UpdateExclusiveAccessBubble(
    const ExclusiveAccessBubbleParams& params,
    ExclusiveAccessBubbleHideCallback first_hide_callback) {
  // Show/Hide full screen reminder bubble based on our settings preference for
  // tab and browser initiated fullscreen.
  if ((params.type ==
           EXCLUSIVE_ACCESS_BUBBLE_TYPE_FULLSCREEN_EXIT_INSTRUCTION ||
       params.type ==
           EXCLUSIVE_ACCESS_BUBBLE_TYPE_BROWSER_FULLSCREEN_EXIT_INSTRUCTION) &&
      !GetProfile()->GetPrefs()->GetBoolean(kShowFullscreenReminder)) {
    return;
  }
  UpdateExclusiveAccessBubble_ChromiumImpl(params,
                                           std::move(first_hide_callback));
}


```

