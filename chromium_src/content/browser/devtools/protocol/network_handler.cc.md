### match
```cpp
...
 
 namespace content { ... 
 
 namespace protocol { ... 
 
 void NetworkHandler::ConfigureDurableMessages(
    std::optional<int> max_total_size,
    std::optional<int> max_resource_size,
    std::unique_ptr<ConfigureDurableMessagesCallback> callback) { ... 
MaybeEnableDurableMessages(base::BindOnce(
      &ConfigureDurableMessagesCallback::sendSuccess, std::move(callback)));
 } 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
void NetworkHandler::RequestAdblockInfoReceived(
    const std::string& request_id,
    std::unique_ptr<protocol::Network::AdblockInfo> info) {
  if (!enabled_) {
    return;
  }
  frontend_->RequestAdblockInfoReceived(request_id, std::move(info));
}

```

