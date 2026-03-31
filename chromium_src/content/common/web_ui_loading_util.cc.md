### match
```cpp
...
// found in the LICENSE file.
 #include "content/common/web_ui_loading_util.h"
 
 >>> 
#include "base/check.h"

 ... 
```
### patch
```cpp
#include "services/network/public/mojom/url_loader.mojom.h"
#include "services/network/public/mojom/url_response_head.mojom.h"

```

### match
```cpp
...
 
 namespace content { ... 
 
 namespace webui { ... 
 
 bool SendData(
    network::mojom::URLResponseHeadPtr headers,
    mojo::PendingRemote<network::mojom::URLLoaderClient> client_remote,
    std::optional<net::HttpByteRange> requested_range,
    scoped_refptr<base::RefCountedMemory> bytes) { ... 
mojo::Remote<network::mojom::URLLoaderClient> client(
      std::move(client_remote));  >>> 
 client->OnReceiveResponse(std::move(headers), std::move(pipe), std::nullopt);  <<< 
network::URLLoaderCompletionStatus status(net::OK);
 ... } ...  } ...  } ...  
```
### patch
```cpp
  client->OnReceiveResponse(UseContentLengthFromHeaders(std::move(headers), std::move(pipe), std::nullopt));

```

### match
```cpp
...
 
 namespace content { ... 
 
 namespace webui { ... 
 
 std::pair<mojo::ScopedDataPipeConsumerHandle, size_t> GetPipe(
    scoped_refptr<base::RefCountedMemory> bytes,
    std::optional<net::HttpByteRange> requested_range) { ... 
return std::make_pair(std::move(pipe_consumer_handle), output_size);
 } 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
namespace {
network::mojom::URLResponseHeadPtr UseContentLengthFromHeaders(
    network::mojom::URLResponseHeadPtr headers) {
  if (auto content_length = headers->headers->GetContentLength();
      content_length && !content_length->is_negative()) {
    headers->content_length = content_length->InBytes();
  }
  return headers;
}

}  // namespace

```

