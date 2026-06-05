### match
```cpp
...
 
 void BookmarkBubbleView::ShowBubble(views::View* anchor_view,
                                    content::WebContents* web_contents,
                                    views::Button* highlighted_button,
                                    Browser* browser,
                                    const GURL& url,
                                    bool already_bookmarked) { ... 
// This is only neceessary for the legacy page action framework.
>>> 
 StarView* star_view = nullptr; 
<<< 
if (!IsPageActionMigrated(PageActionIconType::kBookmarkStar)) {
    star_view = static_cast<StarView*>(highlighted_button);
  }
 ... } ...  
```
### patch
```cpp
  BraveStarView* star_view = nullptr;

```

### match
```cpp
...
 
 void BookmarkBubbleView::ShowBubble(views::View* anchor_view,
                                    content::WebContents* web_contents,
                                    views::Button* highlighted_button,
                                    Browser* browser,
                                    const GURL& url,
                                    bool already_bookmarked) { ... 
 
 if (!IsPageActionMigrated(PageActionIconType::kBookmarkStar)) { ... 
>>> 
 star_view = static_cast<StarView*>(highlighted_button); 
<<< 
...} ...  } ...  
```
### patch
```cpp
    star_view = static_cast<BraveStarView*>(highlighted_button);

```

### match
```cpp
...
 
 void BookmarkBubbleView::ShowBubble(views::View* anchor_view,
                                    content::WebContents* web_contents,
                                    views::Button* highlighted_button,
                                    Browser* browser,
                                    const GURL& url,
                                    bool already_bookmarked) { ... 
auto bubble = std::make_unique<views::BubbleDialogModelHost>(
      dialog_model_builder.Build(), anchor_view,
      views::BubbleBorder::TOP_RIGHT);
 bookmark_bubble_ = bubble.get(); 
 >>> 
bubble->SetHighlightedElement(kBookmarkStarViewElementId);
 ... } ...  
```
### patch
```cpp
  bubble->SetArrow(views::BubbleBorder::TOP_LEFT);

```

