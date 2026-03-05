### match
```
...
// found in the LICENSE file.
 #include "net/socket/ssl_client_socket_impl.h"
 
 >>> 
#include <errno.h>

 ... 
```
### patch
```
#include "net/http/transport_security_state.h"

```

### match
```
...
 namespace net { ... 
 ssl_verify_result_t SSLClientSocketImpl::HandleVerifyResult() { ...   >>> 
 context_->transport_security_state()->ShouldSSLErrorsBeFatal(
          host_and_port_.host()) 
 ;  <<< ... } ...  } ...  
```
### patch
```
      context_->transport_security_state()->ShouldSSLErrorsBeFatal(ssl_config_.network_anonymization_key,host_and_port_.host());

```

