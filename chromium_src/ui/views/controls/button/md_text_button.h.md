### match
```cpp
...
 
 # ifndef ... 
#include <optional>

 #include <string_view>
 
 >>> 
#include "base/functional/callback.h"

 ... 
```
### patch
```cpp
#include "base/gtest_prod_util.h"
#include "third_party/skia/include/core/SkColor.h"
#include "ui/gfx/vector_icon_types.h"
#include "ui/views/controls/button/label_button.h"

```

### match
```cpp
...
>>>
 class VIEWS_EXPORT 
 MdTextButton 
 : public LabelButton 
 { 
 METADATA_HEADER(MdTextButton, LabelButton)  <<<  ...} ...  
```
### patch
```cpp
class VIEWS_EXPORT MdTextButtonBase : public LabelButton {
  METADATA_HEADER(MdTextButtonBase, LabelButton)

```

### match
```cpp
...
>>>
 explicit 
 MdTextButton 
 (  <<< 
PressedCallback callback = PressedCallback()
 ... ) ...  
```
### patch
```cpp
  explicit MdTextButtonBase(

```

### match
```cpp
...
 
 # ifndef ... 
 
 class VIEWS_EXPORT MdTextButtonBase : public LabelButton { ... 
public:
    explicit MdTextButtonBase(
PressedCallback callback = PressedCallback(),
      std::u16string_view text = {},
      int button_context = style::CONTEXT_BUTTON_MD,
      bool use_text_color_for_icon = true,
      std::unique_ptr<LabelButtonImageContainer> image_container =
          std::make_unique<SingleImageContainer>());  >>> 
 MdTextButton(const MdTextButton&) = delete; 
 MdTextButton& operator=(const MdTextButton&) = delete;  <<< 
~MdTextButton() override
 ... } ...  
```
### patch
```cpp
  MdTextButtonBase(const MdTextButtonBase&) = delete;
  MdTextButtonBase& operator=(const MdTextButtonBase&) = delete;

```

### match
```cpp
...
 
 # ifndef ... 
 
 class VIEWS_EXPORT MdTextButtonBase : public LabelButton { ... 
MdTextButtonBase& operator=(const MdTextButtonBase&) = delete;  >>> 
 ~MdTextButton() override 
 ;  <<< 
void SetStyle(ui::ButtonStyle button_style);
 ... } ...  
```
### patch
```cpp

  ~MdTextButtonBase() override;

```

### match
```cpp
...
 
 # ifndef ... 
 
 class VIEWS_EXPORT MdTextButtonBase : public LabelButton { ... 
gfx::Insets CalculateDefaultPadding() const;  >>> 
 void UpdateTextColor();  <<< 
void UpdateBackgroundColor() override;
 ... } ...  
```
### patch
```cpp
 protected:
  virtual void UpdateTextColor();

```

### match
```cpp
...
 
 # ifndef ... 
 
 class VIEWS_EXPORT MdTextButtonActionViewInterface
    : public LabelButtonActionViewInterface { ...   >>> 
 explicit MdTextButtonActionViewInterface(MdTextButton* action_view);  <<<  ...} ...  
```
### patch
```cpp
  explicit MdTextButtonActionViewInterface(MdTextButtonBase* action_view);

```

### match
```cpp
...
 
 # ifndef ... 
 
 class VIEWS_EXPORT MdTextButtonActionViewInterface
    : public LabelButtonActionViewInterface { ...   >>> 
 raw_ptr<MdTextButton> action_view_;  <<<  ...} ...  
```
### patch
```cpp
  raw_ptr<MdTextButtonBase> action_view_;

```

### match
```cpp
...
 
 # ifndef ...   >>> 
 BEGIN_VIEW_BUILDER(VIEWS_EXPORT, MdTextButton, LabelButton)  <<<  ...
```
### patch
```cpp
BEGIN_VIEW_BUILDER(VIEWS_EXPORT, MdTextButtonBase, LabelButton)

```

### match
```cpp
...
 
 # ifndef ... 
// namespace views  >>> 
 DEFINE_VIEW_BUILDER(VIEWS_EXPORT, MdTextButton)  <<<  ...
```
### patch
```cpp
DEFINE_VIEW_BUILDER(VIEWS_EXPORT, MdTextButtonBase)
// Make visual changes to MdTextButton in line with Brave visual style:
//  - Different hover text and boder color for non-prominent button
//  - Different hover bg color for prominent background
//  - No shadow for prominent background
class VIEWS_EXPORT MdTextButton : public MdTextButtonBase {
  METADATA_HEADER(MdTextButton, views::MdTextButtonBase)

 public:
  struct ButtonColors {
    SkColor background_color;
    SkColor stroke_color;
    SkColor text_color;
  };

  explicit MdTextButton(
      PressedCallback callback = PressedCallback(),
      std::u16string_view text = {},
      int button_context = style::CONTEXT_BUTTON_MD,
      bool use_text_color_for_icon = true,
      std::unique_ptr<LabelButtonImageContainer> image_container =
          std::make_unique<SingleImageContainer>());
  MdTextButton(const MdTextButton&) = delete;
  MdTextButton& operator=(const MdTextButton&) = delete;
  ~MdTextButton() override;

  void SetIcon(const gfx::VectorIcon* icon, int icon_size = 0);

  bool GetLoading() const;
  void SetLoading(bool loading);
  void set_use_default_for_tonal(bool use_default) {
    use_default_for_tonal_ = use_default;
  }

  // MdTextButtonBase:
  void UpdateTextColor() override;
  void UpdateBackgroundColor() override;
  void UpdateColors() override;

 private:
  FRIEND_TEST_ALL_PREFIXES(MdTextButtonTest, ButtonColorsTest);

  ButtonColors GetButtonColors();
  ui::ButtonStyle GetBraveStyle() const;

  bool loading_ = false;

  // By default, use kDefault style for kTonal because
  // it's not suitable to our style. Use default style instead.
  bool use_default_for_tonal_ = true;

  int icon_size_ = 0;
  raw_ptr<const gfx::VectorIcon> icon_ = nullptr;
};

}  // namespace views

DEFINE_VIEW_BUILDER(VIEWS_EXPORT, MdTextButton)

```

