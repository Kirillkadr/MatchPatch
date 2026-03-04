### match
```
...
 # ifndef ... 
 namespace version_info { ...   >>> 
 constexpr 
 std::string_view 
 GetChannelString(Channel channel) 
 {  <<< ... 
switch (channel) {
    case Channel::STABLE:
      return "stable";
    case Channel::BETA:
      return "beta";
    case Channel::DEV:
      return "dev";
    case Channel::CANARY:
      return "canary";
    case Channel::UNKNOWN:
      return "unknown";
  }
 ... } ...  } ...  
```
### patch
```
constexpr std::string_view GetChannelString_ChromiumImpl(Channel channel) {

```

### match
```
...
 # ifndef ... 
 namespace version_info { ... 
 constexpr std::string_view GetChannelString_ChromiumImpl(Channel channel) { ... 
NOTREACHED();
 } 
 >>> 
 ... } ...  
```
### patch
```
// We use |nightly| instead of |canary|.
constexpr std::string_view GetChannelString(Channel channel) {
  if (channel == Channel::CANARY) {
    return "nightly";
  }

  return GetChannelString_ChromiumImpl(channel);
}


```

