### match
```cpp
...
#include "chrome/browser/win/mica_titlebar.h"

 #include "chrome/grit/theme_resources.h"
 
 >>> 
#include "ui/color/color_id.h"

 ... 
```
### patch
```cpp
#include "third_party/skia/include/core/SkColor.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 FrameTransforms GetSystemFrameTransforms(const ui::ColorProviderKey& key) { ...   >>> 
 if 
 ( 
 const auto* const accent_color_observer = ui::AccentColorObserver::Get();  <<< 
accent_color_observer->ShouldUseAccentColorForWindowFrame()
 ... ) ...  } ...  } ...  
```
### patch
```cpp
  if (const auto* const accent_color_observer = ui::FakeAccentColorObserver::Get();

```

### match
```cpp
...
 
 namespace { ... 
 
 void EnsureColorProviderCacheWillBeResetWhenAccentColorStateChanges() { ...   >>> 
 ui::AccentColorObserver::Get()->Subscribe 
 ( 
 base::BindRepeating 
 (  <<< 
// CAUTION: Do not bind directly to `ui::ColorProviderManager::Get()`
 ... ) ...  ) ...  } ...  } ...  
```
### patch
```cpp
      ui::FakeAccentColorObserver::Get()->Subscribe(base::BindRepeating(

```

### match
```cpp
...
 
 namespace { ... 
 
 SkColor GetAccentBorderColor() { ...   >>> 
 if 
 ( 
 const auto* const accent_color_observer = ui::AccentColorObserver::Get();  <<< 
accent_color_observer->ShouldUseAccentColorForWindowFrame()
 ... ) ...  } ...  } ...  
```
### patch
```cpp
  if (const auto* const accent_color_observer = ui::FakeAccentColorObserver::Get();

```

### match
```cpp
...
 
 void AddNativeChromeColorMixer(ui::ColorProvider* provider,
                               const ui::ColorProviderKey& key) { ... 
if (key.contrast_mode == ui::ColorProviderKey::ContrastMode::kHigh) {
    AddNativeHighContrastColors(mixer);
  } else {
    AddNativeNonHighContrastColors(mixer, key);
  }
 } 
 >>> 
 ... 
```
### patch
```cpp

namespace ui {

class FakeAccentColorObserver {
 public:
  static FakeAccentColorObserver* Get() {
    static base::NoDestructor<FakeAccentColorObserver> observer;
    return observer.get();
  }

  FakeAccentColorObserver() {}
  FakeAccentColorObserver(const FakeAccentColorObserver&) = delete;
  FakeAccentColorObserver& operator=(const FakeAccentColorObserver&) = delete;
  ~FakeAccentColorObserver() {}

  base::CallbackListSubscription Subscribe(base::RepeatingClosure callback) {
    return callbacks_.Add(std::move(callback));
  }

  std::optional<SkColor> accent_color() const { return std::nullopt; }
  std::optional<SkColor> accent_color_inactive() const { return std::nullopt; }
  std::optional<SkColor> accent_border_color() const { return std::nullopt; }
  bool use_dwm_frame_color() const { return false; }

  bool ShouldUseAccentColorForWindowFrame() const { return false; }

 private:
  base::RepeatingClosureList callbacks_;
};

}  // namespace ui
```

