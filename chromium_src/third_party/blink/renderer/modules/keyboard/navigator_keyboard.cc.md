### match
```
...
// found in the LICENSE file.
 #include "third_party/blink/renderer/modules/keyboard/navigator_keyboard.h"
 
 >>> 
#include "third_party/blink/renderer/core/frame/local_dom_window.h"

 ... 
```
### patch
```
#include "third_party/blink/renderer/modules/keyboard/navigator_keyboard.h"

#include "brave/third_party/blink/renderer/brave_farbling_constants.h"
#include "brave/third_party/blink/renderer/core/farbling/brave_session_cache.h"
#include "third_party/blink/public/platform/web_content_settings_client.h"

```

### match
```
...
 namespace blink { ...   >>> 
 Keyboard 
 * NavigatorKeyboard::keyboard(Navigator& navigator) 
 {  <<< ... 
NavigatorKeyboard* supplement =
      Supplement<Navigator>::From<NavigatorKeyboard>(navigator);
 ... } ...  } ...  
```
### patch
```
Keyboard* NavigatorKeyboard::keyboard_ChromiumImpl(Navigator& navigator) {

```

### match
```
...
 namespace blink { ... 
 void NavigatorKeyboard::Trace(Visitor* visitor) const { ... 
Supplement<Navigator>::Trace(visitor);
 } 
 >>> 
 ... } ...  
```
### patch
```
// static
Keyboard* NavigatorKeyboard::keyboard(Navigator& navigator) {
  if (ExecutionContext* context = navigator.GetExecutionContext()) {
    if (brave::GetBraveFarblingLevelFor(
            context, ContentSettingsType::BRAVE_WEBCOMPAT_KEYBOARD,
            BraveFarblingLevel::OFF) != BraveFarblingLevel::OFF) {
      return nullptr;
    }
  }
  return keyboard_ChromiumImpl(navigator);
}

```

