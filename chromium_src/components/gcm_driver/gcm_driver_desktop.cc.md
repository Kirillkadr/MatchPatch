### match
```cpp
...
 
 namespace gcm { ... 
 
 bool GCMDriverDesktop::TokenTupleComparer::operator()(
    const TokenTuple& a,
    const TokenTuple& b) const { ... 
return std::get<2>(a) < std::get<2>(b);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
BraveGCMDriverDesktop::~BraveGCMDriverDesktop() = default;
void BraveGCMDriverDesktop::SetEnabled(bool enabled) {
  enabled_ = enabled;
  initialized_ = true;
}

GCMClient::Result BraveGCMDriverDesktop::EnsureStarted(
    GCMClient::StartMode start_mode) {
  if (!initialized_ || !enabled_) {
    return GCMClient::GCM_DISABLED;
  }

  return GCMDriverDesktop::EnsureStarted(start_mode);
}

```

