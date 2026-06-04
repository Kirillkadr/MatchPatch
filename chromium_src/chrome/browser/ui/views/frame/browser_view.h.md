### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
 ... 
```
### patch
```cpp
#if BUILDFLAG(IS_WIN)
// On Windows <winuser.h> defines LoadAccelerators
// Using push_macro seems to be causing #undef not to work in Chromium 125.
// Unclear what causes this.
// #pragma push_macro("LoadAccelerators")
#undef LoadAccelerators
#endif

```

### match
```cpp
...
 #include "base/timer/timer.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/brave_browser_window.h"
#include "brave/browser/ui/views/bookmarks/brave_bookmark_bar_view.h"
#include "brave/browser/ui/views/frame/brave_browser_view_layout.h"
#include "brave/browser/ui/views/side_panel/side_panel.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/browser_window.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/exclusive_access/exclusive_access_context.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/views/intent_picker_bubble_view.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/views/side_panel/side_panel.h"

```

### match
```cpp
...
>>>
 class BookmarkBarView 
 ; 
<<< 
...
```
### patch
```cpp
class BraveBookmarkBarView;

```

### match
```cpp
...
>>>
 class BrowserViewLayout 
 ; 
<<< 
...
```
### patch
```cpp
class BraveBrowserViewLayout;

```

### match
```cpp
...
>>>
 class 
 BrowserView 
 : 
 public 
 BrowserWindow 
 , 
<<< 
...
```
### patch
```cpp
class BrowserView : public BraveBrowserWindow,

```

### match
```cpp
...
 
 class BrowserView : public BraveBrowserWindow,
public TabStripModelObserver,
                    public ui::AcceleratorProvider,
                    public views::WidgetDelegate,
                    public views::WidgetObserver,
                    public content::WebContentsObserver,
                    public views::ClientView,
                    public infobars::InfoBarContainer::Delegate,
                    public ImmersiveModeController::Observer,
                    public webapps::AppBannerManager::Observer,
                    public views::FocusChangeListener,
                    public BookmarkBarController::Delegate { ... 
// Bookmark bar may be null, for example for pop-ups.
>>> 
 BookmarkBarView* bookmark_bar() { return bookmark_bar_view_; } 
<<< 
// Returns the do-nothing view which controls the z-order of the find bar
 ... } ...  
```
### patch
```cpp
  BraveBookmarkBarView* bookmark_bar() { return bookmark_bar_view_; }

```

### match
```cpp
...
// Accessor for the BrowserView's TabSearchBubbleHost instance.
>>> 
 TabSearchBubbleHost* GetTabSearchBubbleHost(); 
<<< 
// Accessor for the ExclusiveAccessBubble.
 ... 
```
### patch
```cpp
  virtual TabSearchBubbleHost* GetTabSearchBubbleHost();

```

### match
```cpp
...
// Returns true if the top UI are visible on screen.
>>> 
 bool GetTabStripVisible() const; 
<<< 
// Returns true if the top UI should be drawn.
 ... 
```
### patch
```cpp
  virtual bool GetTabStripVisible() const;

```

### match
```cpp
...
// Returns whether or not strokes should be drawn around and under the tabs.
>>> 
 bool ShouldDrawTabStrokes() const; 
<<< 
// Returns whether the vertical tabstrip is collapsed.
 ... 
```
### patch
```cpp
  virtual bool ShouldDrawTabStrokes() const;

```

### match
```cpp
...
>>>
 BookmarkBarView* GetBookmarkBarView() const; 
<<< 
...
```
### patch
```cpp
  BraveBookmarkBarView* GetBookmarkBarView() const;

```

### match
```cpp
...
>>>
 BrowserViewLayout 
 * GetBrowserViewLayoutForTesting() 
 { 
<<< 
...} ...  
```
### patch
```cpp
  BraveBrowserViewLayout* GetBrowserViewLayoutForTesting() {

```

### match
```cpp
...
 
 class BrowserView : public BraveBrowserWindow,
public TabStripModelObserver,
                    public ui::AcceleratorProvider,
                    public views::WidgetDelegate,
                    public views::WidgetObserver,
                    public content::WebContentsObserver,
                    public views::ClientView,
                    public infobars::InfoBarContainer::Delegate,
                    public ImmersiveModeController::Observer,
                    public webapps::AppBannerManager::Observer,
                    public views::FocusChangeListener,
                    public BookmarkBarController::Delegate { ... 
 friend class BrowserViewLayoutDelegateImplOld; 
 >>> 
 ... } ...  
```
### patch
```cpp
  friend class BraveBrowserView;
  void SetNativeWindowPropertyForWidget(views::Widget* widget);
  virtual bool IsWebPanelContents(content::WebContents* contents);

```

### match
```cpp
...
// web contents.
>>> 
 void ShowSplitView(bool focus_active_view); 
<<< 
// Display only the current active tab's web contents, hiding any previous
 ... 
```
### patch
```cpp
  virtual void ShowSplitView(bool focus_active_view);

```

### match
```cpp
...
// side-by-side display.
>>> 
 void HideSplitView(); 
<<< 
// Update the index of the active split based on the active tab's web
 ... 
```
### patch
```cpp
  virtual void HideSplitView();

```

### match
```cpp
...
// Returns the BrowserViewLayout.
>>> 
 BrowserViewLayout* GetBrowserViewLayout() const; 
<<< 
// Returns the ContentsLayoutManager.
 ... 
```
### patch
```cpp
  BraveBrowserViewLayout* GetBrowserViewLayout() const;

```

### match
```cpp
...
// true if split view is updated and needs a layout.
>>> 
 bool MaybeUpdateSplitView(content::WebContents* contents); 
<<< 
// Prepare and update devtools for the specified WebContents or any devtools
 ... 
```
### patch
```cpp
  virtual bool MaybeUpdateSplitView(content::WebContents* contents);

```

### match
```cpp
...
// updated and needs a layout.
>>> 
 bool MaybeUpdateDevtools(content::WebContents* contents); 
<<< 
// Updates various optional child Views, e.g. Bookmarks Bar, Info Bar
 ... 
```
### patch
```cpp
  virtual bool MaybeUpdateDevtools(content::WebContents* contents);

```

### match
```cpp
...
// use.
>>> 
 void LoadAccelerators(); 
<<< 
// Retrieves the command id for the specified Windows app command.
 ... 
```
### patch
```cpp
  virtual void LoadAccelerators();

```

### match
```cpp
...
// Reparents |top_container_| to |main_container_|.
>>> 
 void ReparentTopContainerForEndOfImmersive(); 
<<< 
// In certain situations, such as immersive mode and touch ui mode on
 ... 
```
### patch
```cpp
  virtual void ReparentTopContainerForEndOfImmersive();

```

### match
```cpp
...
// whenever the touch mode changes.
>>> 
 void MaybeShowReadingListInSidePanelIPH(); 
<<< 
// Attempts to show IPH promo for the tab search toolbar button.
 ... 
```
### patch
```cpp
  virtual void MaybeShowReadingListInSidePanelIPH();

```

### match
```cpp
...
// non-tabbed browsers like popups. May not be visible.
>>> 
 std::unique_ptr<BookmarkBarView> detached_bookmark_bar_view_; 
 raw_ptr<BookmarkBarView> bookmark_bar_view_ = nullptr; 
<<< 
...
```
### patch
```cpp
  std::unique_ptr<BraveBookmarkBarView> detached_bookmark_bar_view_;
  raw_ptr<BraveBookmarkBarView> bookmark_bar_view_ = nullptr;

```

### match
```cpp
...
 #endif 
 // CHROME_BROWSER_UI_VIEWS_FRAME_BROWSER_VIEW_H_ 
 >>> 
 ... 
```
### patch
```cpp
#if BUILDFLAG(IS_WIN)
// #pragma pop_macro("LoadAccelerators")
#endif
```

