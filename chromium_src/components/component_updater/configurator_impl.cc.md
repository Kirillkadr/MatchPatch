### match
```cpp
...
// found in the LICENSE file.
 #include "components/component_updater/configurator_impl.h"
 
 >>> 
#include <algorithm>

 ... 
```
### patch
```cpp
#include "brave/components/update_client/privacy_preserving_protocol_handler.h"

```

### match
```cpp
...
 
 namespace component_updater { ...   >>> 
 bool 
 ConfiguratorImpl::EnabledBackgroundDownloader() const 
 {  <<< 
DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
 ... } ...  } ...  
```
### patch
```cpp
bool ConfiguratorImpl::EnabledBackgroundDownloader_Unused() const {

```

### match
```cpp
...
 
 namespace component_updater { ...   >>> 
 bool 
 ConfiguratorImpl::EnabledCupSigning() const 
 {  <<< 
DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
 ... } ...  } ...  
```
### patch
```cpp
bool ConfiguratorImpl::EnabledCupSigning_Unused() const {

```

### match
```cpp
...
 
 namespace component_updater { ... 
 
 std::unique_ptr<update_client::ProtocolHandlerFactory>
ConfiguratorImpl::GetProtocolHandlerFactory() const { ... 
DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);  >>> 
 return std::make_unique<update_client::ProtocolHandlerFactoryJSON>();  <<<  ...} ...  } ...  
```
### patch
```cpp
  return std::make_unique<update_client::PrivacyPreservingProtocolHandlerFactory>();

```

### match
```cpp
...
 
 namespace component_updater { ... 
 
 bool ConfiguratorImpl::IsConnectionMetered() const { ... 
return net::NetworkChangeNotifier::GetConnectionCost() ==
         net::NetworkChangeNotifier::CONNECTION_COST_METERED;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool ConfiguratorImpl::EnabledBackgroundDownloader() const {
  return false;
}
bool ConfiguratorImpl::EnabledCupSigning() const {
  return false;
}

```

