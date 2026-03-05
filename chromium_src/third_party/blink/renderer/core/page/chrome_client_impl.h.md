### match
```
...
 # ifndef ... 
#define THIRD_PARTY_BLINK_RENDERER_CORE_PAGE_CHROME_CLIENT_IMPL_H_

 #include <memory>
 
 >>> 
#include "base/gtest_prod_util.h"

 ... 
```
### patch
```
#include "third_party/blink/renderer/core/page/chrome_client.h"
#include "ui/display/screen_infos.h"

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT ChromeClientImpl final : public ChromeClient { ... 
float WindowToViewportScalar(LocalFrame*, const float) const override;
 const display::ScreenInfo& GetScreenInfo(LocalFrame&) const override; 
 >>> 
const display::ScreenInfos& GetScreenInfos(LocalFrame&) const override;
 ... } ...  } ...  
```
### patch
```
  const display::ScreenInfos& BraveGetScreenInfos(LocalFrame&) const override;

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT ChromeClientImpl final : public ChromeClient { ... 
ui::Cursor last_set_mouse_cursor_for_testing_;
 bool cursor_overridden_; 
 >>> 
Member<ExternalDateTimeChooser> external_date_time_chooser_;
 ... } ...  } ...  
```
### patch
```
  mutable display::ScreenInfos screen_infos_;

```

