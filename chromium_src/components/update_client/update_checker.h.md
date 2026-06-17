### match
```cpp
...
 #include <vector>
 
 >>> 
 ... 
```
### patch
```cpp
#include <deque>
#include <optional>
#include <string>
#include <vector>

#include "base/containers/flat_map.h"
#include "base/memory/raw_ptr.h"
#include "base/threading/thread_checker.h"
#include "components/update_client/component.h"
#include "components/update_client/configurator.h"
#include "components/update_client/persisted_data.h"
#include "components/update_client/update_client_errors.h"


```

### match
```cpp
...
 
 namespace update_client { ... 
 
 class UpdateChecker { ... 
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
class SequentialUpdateChecker : public UpdateChecker {
 public:
  static std::unique_ptr<UpdateChecker> Create(
      scoped_refptr<Configurator> config);

  void CheckForUpdates(
      scoped_refptr<UpdateContext> update_context,
      const base::flat_map<std::string, std::string>& additional_attributes,
      UpdateCheckCallback update_check_callback) override;

  // Needs to be public so std::make_unique(...) works in Create(...).
  explicit SequentialUpdateChecker(scoped_refptr<Configurator> config);
  SequentialUpdateChecker(const SequentialUpdateChecker&) = delete;
  SequentialUpdateChecker& operator=(const SequentialUpdateChecker&) = delete;
  ~SequentialUpdateChecker() override;

 private:
  void CheckNext();
  void UpdateResultAvailable(std::optional<ProtocolParser::Results> results,
                             ErrorCategory error_category,
                             int error,
                             int retry_after_sec);

  THREAD_CHECKER(thread_checker_);

  const scoped_refptr<Configurator> config_;

  // This update conext instance is stored locally and then used to create
  // individidual UpdateContext instances based on each application id.
  scoped_refptr<UpdateContext> update_context_;

  base::flat_map<std::string, std::string> additional_attributes_;
  UpdateCheckCallback update_check_callback_;

  std::deque<std::string> remaining_ids_;

  // The currently running update_checker_. We keep a smart pointer to it to
  // keep it alive while this particular sequential update check takes place.
  std::unique_ptr<UpdateChecker> update_checker_;
  // Aggregates results from all sequential update requests.
  ProtocolParser::Results results_;
};

```

