### match
```
...
 # ifndef ... 
#include <stddef.h>

 #include <stdint.h>
 
 >>> 
#include <memory>

 ... 
```
### patch
```
#include <memory>
#include <string>

```

### match
```
...
 # ifndef ... 
#include <memory>

 #include <string>
 
 >>> 
#include "base/memory/scoped_refptr.h"

 ... 
```
### patch
```
#include "net/socket/transport_connect_job.h"

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT_PRIVATE SOCKS5ClientSocket : public StreamSocket { ... 
NetworkTrafficAnnotationTag traffic_annotation_;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```
class NET_EXPORT_PRIVATE SOCKS5ClientSocketAuth : public SOCKS5ClientSocket {
 public:
  SOCKS5ClientSocketAuth(std::unique_ptr<StreamSocket> transport_socket,
                         const HostPortPair& destination,
                         const NetworkTrafficAnnotationTag& traffic_annotation,
                         const TransportSocketParams::Endpoint& proxy_endpoint);
  SOCKS5ClientSocketAuth(const SOCKS5ClientSocketAuth&) = delete;
  SOCKS5ClientSocketAuth& operator=(const SOCKS5ClientSocketAuth&) = delete;
  ~SOCKS5ClientSocketAuth() override;

 private:
  bool do_auth();
  const std::string& username();
  const std::string& password();
  uint8_t auth_method() override;
  int Authenticate(int rv,
                   NetLogWithSource& net_log,
                   CompletionRepeatingCallback& callback) override;
  const HostPortPair proxy_host_port_;
  enum {
    STATE_INIT_WRITE = 0,
    STATE_WRITE,
    STATE_WRITE_COMPLETE,
    STATE_INIT_READ,
    STATE_READ,
    STATE_READ_COMPLETE,
    STATE_DONE,
    STATE_BAD,
  } next_state_;
  scoped_refptr<IOBuffer> iobuf_;
  std::string buffer_;
  size_t buffer_left_;
};

```

