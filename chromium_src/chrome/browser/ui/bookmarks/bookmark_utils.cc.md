### match
```cpp
...
#include "base/notreached.h"

 #include "base/strings/utf_string_conversions.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/resources/bookmark_icon/grit/bookmark_icon_resources.h"
#include "brave/browser/ui/bookmark/bookmark_helper.h"
#include "brave/browser/ui/brave_ui_features.h"
#include "brave/components/constants/pref_names.h"

```

### match
```cpp
...
#include "chrome/browser/profiles/profile.h"

 #include "chrome/browser/search/search.h"
 
 >>> 
#include "chrome/browser/ui/ui_features.h"

 ... 
```
### patch
```cpp
#include "chrome/browser/ui/color/chrome_color_id.h"

```

### match
```cpp
...
#include "components/user_prefs/user_prefs.h"

 #include "components/vector_icons/vector_icons.h"
 
 >>> 
#include "content/public/browser/web_contents.h"

 ... 
```
### patch
```cpp
#include "content/public/browser/browser_context.h"

```

### match
```cpp
...
#include "ui/base/dragdrop/mojom/drag_drop_types.mojom.h"

 #include "ui/base/l10n/l10n_util.h"
 
 >>> 
#include "ui/base/pointer/touch_ui_controller.h"

 ... 
```
### patch
```cpp
#include "ui/base/models/image_model.h"

```

### match
```cpp
...
#include "ui/base/models/image_model.h"

 #include "ui/base/pointer/touch_ui_controller.h"
 
 >>> 
#include "ui/base/ui_base_features.h"

 ... 
```
### patch
```cpp
#include "ui/base/resource/resource_bundle.h"

```

### match
```cpp
...
#include "ui/base/resource/resource_bundle.h"

 #include "ui/base/ui_base_features.h"
 
 >>> 
#include "ui/color/color_variant.h"

 ... 
```
### patch
```cpp
#include "ui/color/color_id.h"

```

### match
```cpp
...
#include "ui/color/color_id.h"

 #include "ui/color/color_variant.h"
 
 >>> 
#if defined(TOOLKIT_VIEWS)
#include "chrome/grit/theme_resources.h"
#include "ui/base/resource/resource_bundle.h"
#include "ui/base/themed_vector_icon.h"
#include "ui/color/color_id.h"
#include "ui/color/color_provider.h"
#include "ui/gfx/canvas.h"
#include "ui/gfx/color_utils.h"
#include "ui/gfx/image/image_skia.h"
#include "ui/gfx/image/image_skia_rep.h"
#include "ui/gfx/image/image_skia_source.h"
#include "ui/gfx/paint_vector_icon.h"
#include "ui/gfx/scoped_canvas.h"
#include "ui/resources/grit/ui_resources.h"
#endif
 ... 
```
### patch
```cpp
#include "ui/color/color_provider.h"
#include "ui/gfx/color_utils.h"

```

### match
```cpp
...
#include "ui/resources/grit/ui_resources.h"

 #endif 
 >>> 
 ... 
```
### patch
```cpp
#if defined(TOOLKIT_VIEWS)
#define GetBookmarkFolderIcon GetBookmarkFolderIcon_UnUsed
#endif

```

### match
```cpp
...
 
 namespace chrome { ... 
 
 bool GetURLAndTitleToBookmark(content::WebContents* web_contents,
                              GURL* url,
                              std::u16string* title) { ... 
return true;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void ToggleBookmarkBarWhenVisible_ChromiumImpl(
    content::BrowserContext* browser_context);

void BraveToggleBookmarkBarState(content::BrowserContext* browser_context) {
  ToggleBookmarkBarWhenVisible_ChromiumImpl(browser_context);
  auto* prefs = user_prefs::UserPrefs::Get(browser_context);
  // On macOS with the View menu or via hotkeys, the options Always show
  // bookmarks is a checkbox. We will keep that checkbox to be Always and Never.
  const bool always_show =
      prefs->GetBoolean(bookmarks::prefs::kShowBookmarkBar);
  brave::SetBookmarkState(always_show ? brave::BookmarkBarState::kAlways
                                      : brave::BookmarkBarState::kNever,
                          prefs);
}


```

### match
```cpp
...
 
 namespace chrome { ... 
 void 
 ToggleBookmarkBarWhenVisible(content::BrowserContext* browser_context) 
 { 
 >>> 
PrefService* prefs = user_prefs::UserPrefs::Get(browser_context);
 ... } ...  } ...  
```
### patch
```cpp
    BraveToggleBookmarkBarState(browser_context);
  }
void ToggleBookmarkBarWhenVisible_ChromiumImpl(content::BrowserContext* browser_context) {

```

### match
```cpp
...
 
 namespace chrome { ... 
 
 bool IsAppsShortcutEnabled(Profile* profile) { ...   >>> 
 #if 
 BUILDFLAG(IS_CHROMEOS) 
 
 
 // Chrome OS uses the app list / app launcher.  <<< 
return false;
 ... } ...  } ...  
```
### patch
```cpp

```

### match
```cpp
...
 
 namespace chrome { ... 
 
 bool IsAppsShortcutEnabled(Profile* profile) { ... 
return false;  >>> 
 #else
 
 return search::IsInstantExtendedAPIEnabled() && !profile->IsOffTheRecord(); 
 #endif
  <<<  ...} ...  } ...  
```
### patch
```cpp

```

### match
```cpp
...
 
 namespace chrome { ... 
 
 bool ShouldShowAppsShortcutInBookmarkBar(Profile* profile) { ...   >>> 
 return IsAppsShortcutEnabled(profile) &&
         profile->GetPrefs()->GetBoolean(
             bookmarks::prefs::kShowAppsShortcutInBookmarkBar);  <<<  ...} ...  } ...  
```
### patch
```cpp
  return false;

```

### match
```cpp
...
 
 namespace chrome { ... 
 
 bool ShouldShowAppsShortcutInBookmarkBar(Profile* profile) { ... 
return false;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
#if defined(TOOLKIT_VIEWS)

ui::ImageModel GetFilledBookmarkFolderIcon(BookmarkFolderIconType icon_type,
                                           ui::ColorVariant color) {
  int default_id = IDR_BRAVE_BOOKMARK_FOLDER_CLOSED_LIGHT;

  const auto generator = [](int default_id, BookmarkFolderIconType icon_type,
                            ui::ColorVariant color,
                            const ui::ColorProvider* color_provider) {
    gfx::ImageSkia folder;
    SkColor sk_color = color.ResolveToSkColor(color_provider);

    const int resource_id = color_utils::IsDark(sk_color)
                                ? IDR_BRAVE_BOOKMARK_FOLDER_CLOSED_LIGHT
                                : IDR_BRAVE_BOOKMARK_FOLDER_CLOSED_DARK;
    folder = *ui::ResourceBundle::GetSharedInstance()
                  .GetNativeImageNamed(resource_id)
                  .ToImageSkia();
    return gfx::ImageSkia(std::make_unique<RTLFlipSource>(folder),
                          folder.size());
  };
  const gfx::Size size =
      ui::ResourceBundle::GetSharedInstance().GetImageNamed(default_id).Size();
  return ui::ImageModel::FromImageGenerator(
      base::BindRepeating(generator, default_id, icon_type, std::move(color)),
      size);
}

ui::ImageModel GetBookmarkFolderIcon(BookmarkFolderIconType icon_type,
                                     ui::ColorVariant color) {
  // If the flag is enabled, use the old "filled" bookmark icon.
  if (base::FeatureList::IsEnabled(features::kBraveFilledBookmarkFolderIcon)) {
    return GetFilledBookmarkFolderIcon(icon_type, color);
  }

  const gfx::VectorIcon* id = icon_type == BookmarkFolderIconType::kManaged
                                  ? &vector_icons::kFolderManagedRefreshIcon
                                  : &vector_icons::kFolderChromeRefreshIcon;
  // Use toolbar icon color for visual consistency with other toolbar icons.
  return ui::ImageModel::FromVectorIcon(*id, kColorToolbarButtonIcon, 20);
}

#endif  // defined(TOOLKIT_VIEWS)


```

### match
```cpp
...
 
 namespace chrome { ... 
#if defined(TOOLKIT_VIEWS)

ui::ImageModel GetBookmarkFolderIcon(BookmarkFolderIconType icon_type,
                                     ui::ColorVariant color) {
  const gfx::VectorIcon* icon_id;
  if (icon_type == BookmarkFolderIconType::kNormal) {
    icon_id = &vector_icons::kFolderChromeRefreshIcon;
  } else {
    icon_id = &vector_icons::kFolderManagedRefreshIcon;
  }
  return ui::ImageModel::FromVectorIcon(*icon_id, color);
}
#endif
 } 
 // namespace chrome 
 >>> 
 ... 
```
### patch
```cpp

#if defined(TOOLKIT_VIEWS)
#undef GetBookmarkFolderIcon
#endif  // defined(TOOLKIT_VIEWS)
```

