### match
```cpp
...
 
 namespace network { ... 
 
 int ResolveHostRequest::Start(
    mojo::PendingReceiver<mojom::ResolveHostHandle> control_handle_receiver,
    mojo::PendingRemote<mojom::ResolveHostClient> pending_response_client,
    net::CompletionOnceCallback callback) { ... 
 if 
 (rv != net::ERR_IO_PENDING) 
 { 
 >>> 
response_client->OnComplete(rv, GetResolveErrorInfo(), GetAddressResults(),
                                GetAlternativeEndpoints());
 ... } ...  } ...  } ...  
```
### patch
```cpp
    if (!internal_request_->GetTextResults().empty()) {         
    response_client->OnTextResults(
        base::ToVector(internal_request_->GetTextResults()));
  }

```

