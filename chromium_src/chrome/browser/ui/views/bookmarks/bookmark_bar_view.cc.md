### match
```cpp
...
#include <vector>

 #include "base/callback_list.h"
 
 >>> 
#include "base/check_op.h"

 ... 
```
### patch
```cpp
#include "base/check.h"

```

### match
```cpp
...
#include "base/task/single_thread_task_runner.h"

 #include "base/time/time.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/brave_view_ids.h"
#include "brave/browser/ui/views/bookmarks/bookmark_bar_instructions_view.h"
#include "brave/browser/ui/views/bookmarks/brave_bookmark_context_menu.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 END_METADATA

// BookmarkFolderButton -------------------------------------------------------

// Buttons used for folders on the bookmark bar, including the 'other folders'
// button.
class BookmarkFolderButton : public BookmarkMenuButtonBase { ... 
BookmarkFolderButton(const BookmarkFolderButton&) = delete;
 BookmarkFolderButton& operator=(const BookmarkFolderButton&) = delete; 
 >>> 
void UpdateCachedTooltipText() { SetTooltipText(GetAccessibleText()); }
 ... } ...  } ...  
```
### patch
```cpp
  constexpr int kBookmarkBarInstructionsPadding = 6;

BookmarkBarInstructionsView* GetInstructionView(
    views::View* bookmark_bar_view) {
  for (views::View* child : bookmark_bar_view->children()) {
    if (child->GetID() == BRAVE_VIEW_ID_BOOKMARK_IMPORT_INSTRUCTION_VIEW)
      return static_cast<BookmarkBarInstructionsView*>(child);
  }
  return nullptr;
}

void LayoutBookmarkBarInstructionsView(views::View* bookmark_bar_view,
                                       bookmarks::BookmarkModel* model,
                                       Browser* browser,
                                       int button_height,
                                       int x,
                                       int max_x,
                                       int y) {
  // Parent view is not ready to layout bookmark bar instruction view.
  if (max_x <= 0)
    return;

  DCHECK(bookmark_bar_view);
  DCHECK(model);
  DCHECK(browser);

  const bool show_instructions =
      model->loaded() && model->bookmark_bar_node()->children().empty();
  views::View* import_instruction_view = GetInstructionView(bookmark_bar_view);
  if (show_instructions) {
    DCHECK_GE(button_height, 0);
    DCHECK_GE(x, 0);
    DCHECK_GE(y, 0);

    if (!import_instruction_view) {
      import_instruction_view = new BookmarkBarInstructionsView(browser);
      bookmark_bar_view->AddChildView(import_instruction_view);
    }
    import_instruction_view->SetVisible(true);
    gfx::Size pref = import_instruction_view->GetPreferredSize();
    import_instruction_view->SetBounds(
        x + kBookmarkBarInstructionsPadding, y,
        std::min(static_cast<int>(pref.width()), max_x - x), button_height);
  } else {
    if (import_instruction_view)
      import_instruction_view->SetVisible(false);
  }
}


```

### match
```cpp
...
 
 void BookmarkBarView::Layout(PassKey) { ... 
 
 if (bookmark_bar_children_count) { ... 
for (size_t i = 0; i <= button_count; ++i) {
      if (i == button_count) {
        // Add another button if there is room for it (and there is another
        // button to load).
        if (!can_render_button_bounds ||
            bookmark_bar_children.size() <= button_count) {
          break;
        }
        InsertBookmarkButtonAtIndex(
            CreateBookmarkButton(bookmark_bar_children[i], i), i);
        button_count = bookmark_buttons_.size();
      }
      views::View* child = bookmark_buttons_[i].first;

      // If the child view can fit in the bookmarks comfortably, make it visible
      // and set its bounds.
      gfx::Size pref = child->GetPreferredSize();
      int next_x = x + pref.width() + bookmark_bar_button_padding;
      can_render_button_bounds = next_x < max_x;
      child->SetVisible(can_render_button_bounds);
      // Only need to set bounds if the view is actually visible.
      if (can_render_button_bounds) {
        child->SetBounds(x, y, pref.width(), button_height);
      }
      x = next_x;
    }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
  LayoutBookmarkBarInstructionsView(this, bookmark_service_->bookmark_model(), \
                                    browser(), button_height, x, max_x, y);

```

### match
```cpp
...
>>>
 context_menu_ 
 = 
 std::make_unique<BookmarkContextMenu> 
 ( 
<<< 
GetWidget()
 ... ) ...  
```
### patch
```cpp
  context_menu_ = std::make_unique<BraveBookmarkContextMenu>(

```

