### match
```cpp
...
 
 # ifndef ... 
 #define COMPONENTS_CONTENT_SETTINGS_RENDERER_CONTENT_SETTINGS_AGENT_IMPL_H_
 
 >>> 
#include <string>

 ... 
```
### patch
```cpp
#include "third_party/blink/public/platform/web_content_settings_client.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
 
 class ContentSettingsAgentImpl
    : public content::RenderFrameObserver,
      public content::RenderFrameObserverTracker<ContentSettingsAgentImpl>,
      public blink::WebContentSettingsClient,
      public mojom::ContentSettingsAgent { ... 
 const blink::WebURL& url 
 ) 
 override 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  bool HasContentSettingsRules() const override;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
 
 class ContentSettingsAgentImpl
    : public content::RenderFrameObserver,
      public content::RenderFrameObserverTracker<ContentSettingsAgentImpl>,
      public blink::WebContentSettingsClient,
      public mojom::ContentSettingsAgent { ... 
mojo::AssociatedReceiverSet<mojom::ContentSettingsAgent> receivers_;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
ContentSetting GetContentSettingFromRulesImpl(
    const ContentSettingsForOneType& rules,
    const GURL& secondary_url);

```

### match
```cpp
...
 
 # ifndef ... 
 #define COMPONENTS_CONTENT_SETTINGS_RENDERER_CONTENT_SETTINGS_AGENT_IMPL_H_
 
 >>> 
#include <string>

 ... 
```
### patch
```cpp
#include "third_party/blink/public/platform/web_content_settings_client.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
 
 class ContentSettingsAgentImpl
    : public content::RenderFrameObserver,
      public content::RenderFrameObserverTracker<ContentSettingsAgentImpl>,
      public blink::WebContentSettingsClient,
      public mojom::ContentSettingsAgent { ... 
 const blink::WebURL& url 
 ) 
 override 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  bool HasContentSettingsRules() const override;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
 
 class ContentSettingsAgentImpl
    : public content::RenderFrameObserver,
      public content::RenderFrameObserverTracker<ContentSettingsAgentImpl>,
      public blink::WebContentSettingsClient,
      public mojom::ContentSettingsAgent { ... 
mojo::AssociatedReceiverSet<mojom::ContentSettingsAgent> receivers_;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
ContentSetting GetContentSettingFromRulesImpl(
    const ContentSettingsForOneType& rules,
    const GURL& secondary_url);

```

