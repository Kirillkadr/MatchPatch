

### match
```cpp

...
#include "ui/views/style/typography_provider.h"

 #include "ui/views/view.h"
 
 >>> 
namespace views 
 ...
```

### patch

```cpp

namespace gfx {

gfx::Insets BraveAdjustVisualBorderForFont(const gfx::FontList& badge_font,
                                           const gfx::Insets& desired_insets) {
  return gfx::Insets::VH(3, 8);
}

}  // namespace gfx
```


### match
```cpp

...
 namespace views { ... 
 namespace { ... 
 >>> 
 badge_rect.Inset (- gfx::AdjustVisualBorderForFont <<< ...  ) ...  } ...  } ...  
```

### patch

```cpp

badge_rect.Inset(-gfx::BraveAdjustVisualBorderForFont(
```
### match
```cpp

...
 namespace views { ... 
 void BadgePainter::PaintBadge(gfx::Canvas* canvas,
                              const View* view,
                              int unmirrored_badge_left_x,
                              int text_top_y,
                              const std::u16string& text,
                              const gfx::FontList& primary_font) { ... 
 color_provider->GetColor(ui::kColorBadgeBackground) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp

  flags.setAntiAlias(true);

```


