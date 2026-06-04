### match
```cpp
...
#include "ui/base/l10n/l10n_util.h"

 #include "ui/base/ui_base_features.h"
 
 >>> 
#include "ui/views/accessibility/view_accessibility.h"

 ... 
```
### patch
```cpp
#include "ui/compositor/layer.h"

```

### match
```cpp
...
#include "ui/compositor/layer.h"

 #include "ui/views/accessibility/view_accessibility.h"
 
 >>> 
#include "ui/views/widget/tooltip_manager.h"

 ... 
```
### patch
```cpp
#include "ui/views/controls/highlight_path_generator.h"

```

### match
```cpp
...
 
 BookmarkButtonBase::BookmarkButtonBase(PressedCallback callback,
                                       std::u16string_view title)
    : LabelButton(std::move(callback), title) { ... 
SetImageLabelSpacing(
      GetLayoutConstant(LayoutConstant::kBookmarkBarButtonImageLabelPadding));
>>> 
 views::InstallPillHighlightPathGenerator(this); 
<<< 
SetFocusBehavior(FocusBehavior::ACCESSIBLE_ONLY);
 ... } ...  
```
### patch
```cpp
  views::Label* bookmark_label = label();                    
  bookmark_label->SetPaintToLayer();
  bookmark_label->SetSubpixelRenderingEnabled(false);
  bookmark_label->layer()->SetFillsBoundsOpaquely(false);

```

