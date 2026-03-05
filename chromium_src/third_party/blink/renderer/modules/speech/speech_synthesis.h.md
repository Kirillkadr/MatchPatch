### match
```
...
 # ifndef ... 
 #define THIRD_PARTY_BLINK_RENDERER_MODULES_SPEECH_SPEECH_SYNTHESIS_H_
 
 >>> 
#include "third_party/blink/public/mojom/speech/speech_synthesis.mojom-blink-forward.h"

 ... 
```
### patch
```
// We need to include this here before redefining OnSetVoiceList to avoid a
// name collision with a method in the mojom class.
#include "third_party/blink/public/mojom/speech/speech_synthesis.mojom-blink.h"

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
void Trace(Visitor*) const override;
 // mojom::blink::SpeechSynthesisVoiceListObserver 
 >>> 
void OnSetVoiceList(
      Vector<mojom::blink::SpeechSynthesisVoicePtr> voices) override;
 ... } ...  
```
### patch
```
  void OnSetVoiceList_ChromiumImpl(                               \
      Vector<mojom::blink::SpeechSynthesisVoicePtr> voices); \

```

