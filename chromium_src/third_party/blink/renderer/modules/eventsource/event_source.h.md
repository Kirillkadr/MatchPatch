### match
```
...
 # ifndef ... 
 #define THIRD_PARTY_BLINK_RENDERER_MODULES_EVENTSOURCE_EVENT_SOURCE_H_
 
 >>> 
#include "base/memory/scoped_refptr.h"

 ... 
```
### patch
```
// Avoid redefining tokens in these headers:
#include "third_party/blink/renderer/core/html/closewatcher/close_watcher.h"
#include "third_party/blink/renderer/core/loader/threadable_loader_client.h"
#include "third_party/blink/renderer/platform/bindings/script_state.h"

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
DEFINE_ATTRIBUTE_EVENT_LISTENER(error, kError)
 void close(); 
 >>> 
const AtomicString& InterfaceName() const override;
 ... } ...  
```
### patch
```
  void close_ChromiumImpl();

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
void DidReceiveData(base::span<const char>) override;
 void DidFinishLoading(uint64_t) override; 
 >>> 
void DidFail(uint64_t, const ResourceError&) override;
 ... } ...  
```
### patch
```
  void DidFail_ChromiumImpl(uint64_t, const ResourceError&);

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
void DidFail_ChromiumImpl(uint64_t, const ResourceError&);
 void DidFail(uint64_t, const ResourceError&) override; 
 >>> 
void DidFailRedirectCheck(uint64_t) override;
 ... } ...  
```
### patch
```
  void MaybeResetEventSourceInUseTracker();
  void DidFailRedirectCheck_ChromiumImpl(uint64_t);

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
void ScheduleInitialConnect();
 void Connect(); 
 >>> 
void NetworkRequestEnded();
 ... } ...  
```
### patch
```
  void BraveConnect();

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
void ScheduleReconnect();
 void ConnectTimerFired(TimerBase*); 
 >>> 
void AbortConnectionAttempt();
 ... } ...  
```
### patch
```
  void ConnectTimerFired_ChromiumImpl(TimerBase*);

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
// because EventSource::Connect can be triggered by |connect_timer_|.
 Member<const DOMWrapperWorld> world_; 
 >>> 
 ... } ...  
```
### patch
```
  std::unique_ptr<ResourcePoolLimiter::ResourceInUseTracker>
      event_source_in_use_tracker_;

```

