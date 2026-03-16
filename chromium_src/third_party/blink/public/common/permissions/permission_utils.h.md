### match
```cpp

...
 # ifndef ... 
 namespace blink { ... 
 enum class PermissionType { ... 
 // Always keep this at the end. 
 >>> 
NUM
 ... } ...  } ...  
```
### patch
```cpp


  BRAVE_ADS,
  BRAVE_TRACKERS,
  BRAVE_HTTP_UPGRADABLE_RESOURCES,
  BRAVE_FINGERPRINTING_V2,
  BRAVE_SHIELDS,
  BRAVE_REFERRERS,
  BRAVE_COOKIES,
  BRAVE_SPEEDREADER,
  BRAVE_ETHEREUM,
  BRAVE_SOLANA,
  BRAVE_GOOGLE_SIGN_IN,
  BRAVE_OPEN_AI_CHAT,
  BRAVE_CARDANO,

```

### match
```cpp

...
 # ifndef ... 
 namespace blink { ... 
 NUM 
 , 
 >>> 
MIN_VALUE = MIDI_SYSEX
 ... } ...  
```
### patch
```cpp

  BRAVE_MIN_VALUE = BRAVE_ADS
// clang-format on

```

