### match
```
...
 namespace blink { ... 
 if (!frame)
      return;
 >>>  ...  } ...
```
### patch
```
    frame->IsFrameCreatedByAdScript(); /* no-op */
  base::AutoReset<String> ephemeral_name_auto_reset(
      &name_, GetEphemeralBroadcastChannelName(window, name_)); 

```

### match
```
...
 namespace blink { ... 
 bool BroadcastChannel::IsRemoteClientConnectedForTesting() const { ... 
return remote_client_.is_connected();
 } 
 >>> 
 ... } ...  
```
### patch
```
namespace {
String GetEphemeralBroadcastChannelName(LocalDOMWindow* window, String name) {
  auto* ephemeral_storage_origin = GetEphemeralStorageOrigin(window);
  if (!ephemeral_storage_origin) {
    return name;
  }
  const auto& nonce = SecurityOrigin::GetNonceForEphemeralStorageKeying(
      ephemeral_storage_origin);
  return name + String::FromUTF8(nonce.ToString());
}

}  // namespace

```

