### match
```
...
#include "third_party/blink/renderer/platform/wtf/threading.h"

 #endif 
 >>> 
 ... 
```
### patch
```
#define userAgent userAgent_ChromiumImpl

```

### match
```
...
 namespace 
 blink 
 { 
 >>> 
namespace {

String GetReducedNavigatorPlatform() {
#if BUILDFLAG(IS_ANDROID)
  return "Linux armv81";
#elif BUILDFLAG(IS_MAC)
  return "MacIntel";
#elif BUILDFLAG(IS_WIN)
  return "Win32";
#elif BUILDFLAG(IS_FUCHSIA)
  return "";
#elif BUILDFLAG(IS_LINUX) || BUILDFLAG(IS_CHROMEOS)
  return "Linux x86_64";
#elif BUILDFLAG(IS_IOS)
  return "iPhone";
#else
#error Unsupported platform
#endif
}

}
 ... } ...  
```
### patch
```
namespace probe {
void ApplyBraveHardwareConcurrencyOverride(blink::ExecutionContext* context,
                                           unsigned int* hardware_concurrency) {
  static constexpr unsigned kFakeMinProcessors = 2;
  static constexpr unsigned kFakeMaxProcessors = 8;
  unsigned true_value =
      static_cast<unsigned>(base::SysInfo::NumberOfProcessors());
  if (true_value <= 2) {
    *hardware_concurrency = true_value;
    return;
  }
  unsigned farbled_value = true_value;
  switch (brave::GetBraveFarblingLevelFor(
      context, ContentSettingsType::BRAVE_WEBCOMPAT_HARDWARE_CONCURRENCY,
      BraveFarblingLevel::OFF)) {
    case BraveFarblingLevel::OFF: {
      break;
    }
    case BraveFarblingLevel::MAXIMUM: {
      true_value = kFakeMaxProcessors;
      // "Maximum" behavior is "balanced" behavior but with a fake maximum,
      // so fall through here.
      [[fallthrough]];
    }
    case BraveFarblingLevel::BALANCED: {
      brave::FarblingPRNG prng =
          brave::BraveSessionCache::From(*context).MakePseudoRandomGenerator();
      farbled_value =
          kFakeMinProcessors + (prng() % (true_value + 1 - kFakeMinProcessors));
      break;
    }
    default:
      NOTREACHED();
  }
  *hardware_concurrency = farbled_value;
}
}

```

### match
```
...
 namespace blink { ... 
 unsigned int NavigatorBase::hardwareConcurrency() const { ... 
 NavigatorConcurrentHardware::hardwareConcurrency() 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```
  probe::ApplyBraveHardwareConcurrencyOverride(GetExecutionContext(),
                                        &hardware_concurrency);

```

### match
```
...
 namespace blink { ... 
 UserAgentMetadata NavigatorBase::GetUserAgentMetadata() const { ... 
return execution_context ? execution_context->GetUserAgentMetadata()
                           : blink::UserAgentMetadata();
 } 
 >>> 
 ... } ...  
```
### patch
```
String NavigatorBase::userAgent() const {
  if (ExecutionContext* context = GetExecutionContext()) {
    if (!brave::AllowFingerprinting(
            context, ContentSettingsType::BRAVE_WEBCOMPAT_USER_AGENT)) {
      return brave::BraveSessionCache::From(*context).FarbledUserAgent(
          context->UserAgent());
    }
  }
  return userAgent_ChromiumImpl();
}

```

