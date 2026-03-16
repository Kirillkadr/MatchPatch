### match
```cpp

...
 namespace net { ... 
 namespace { ... 
// This function converts the binary hashes to a base64 string which we can
 // include in a JSON file. 
 >>> 
std::string HashedDomainToExternalString(
    const TransportSecurityState::HashedHost& hashed) {
  return base::Base64Encode(hashed);
}
 ... } ...  } ...  
```
### patch
```cpp

// Use upstream version of TransportSerurityState to reference
// TransportSecurityState::Delegate without build issues.
#define TransportSecurityState TransportSecurityState_ChromiumImpl

```

### match
```cpp

...
 namespace net { ... 
void TransportSecurityPersister::CompleteLoad(const std::string& state) {
  DCHECK(foreground_runner_->RunsTasksInCurrentSequence());

  if (state.empty())
    return;

  LoadEntries(state);
}
 } 
 // namespace net 
 >>> 
 ... 
```
### patch
```cpp

#undef TransportSecurityState

```

