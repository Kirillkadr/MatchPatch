### match
```cpp
...
 
 # ifndef ... 
#include <string>

 #include <vector>
 
 >>> 
#include "base/files/file_path.h"

 ...
```
### patch
```cpp
#include "components/update_client/update_client.h"

```

### match
```cpp
...
 >>> 
virtual bool AllowUpdatesOnMeteredConnections() const;
 ...
```
### patch
```cpp
  virtual bool IsBraveComponent() const;              

```

### match
```cpp
...
void Install(const base::FilePath& unpack_path,
               const std::string& public_key,
               std::unique_ptr<InstallParams> install_params,
               ProgressCallback progress_callback,
               Callback callback) override; 
 >>> 
 ...
```
### patch
```cpp
  void Register_ChromiumImpl(ComponentUpdateService* cus,
                             base::OnceClosure callback);
  void Register_ChromiumImpl(
      RegisterCallback register_callback, base::OnceClosure callback,
      const base::Version& registered_version = base::Version(kNullVersion),
      const base::Version& max_previous_product_version =
          base::Version(kNullVersion));
  bool IsBraveComponent() const override;

```

