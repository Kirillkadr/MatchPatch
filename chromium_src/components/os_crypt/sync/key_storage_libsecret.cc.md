### match
```cpp
...
#include "build/branding_buildflags.h"

 #include "components/os_crypt/sync/libsecret_util_linux.h"
 
 >>> 
namespace {

const SecretSchema kKeystoreSchemaV2 = {
    "chrome_libsecret_os_crypt_password_v2",
    SECRET_SCHEMA_DONT_MATCH_NAME,
    {
        {"application", SECRET_SCHEMA_ATTRIBUTE_STRING},
        {nullptr, SECRET_SCHEMA_ATTRIBUTE_STRING},
    }};

// From a search result, extracts a SecretValue, asserting that there was at
// most one result. Returns nullptr if there are no results.
SecretValue* ToSingleSecret(GList* secret_items) {
  GList* first = g_list_first(secret_items);
  if (first == nullptr)
    return nullptr;
  if (g_list_next(first) != nullptr) {
    VLOG(1) << "OSCrypt found more than one encryption keys.";
  }
  SecretItem* secret_item = static_cast<SecretItem*>(first->data);
  SecretValue* secret_value =
      LibsecretLoader::secret_item_get_secret(secret_item);
  return secret_value;
}

// Checks the timestamps of the secret item and prints findings to logs. We
// presume that at most one secret item can be present.
void AnalyseKeyHistory(GList* secret_items) {
  GList* first = g_list_first(secret_items);
  if (first == nullptr)
    return;

  SecretItem* secret_item = static_cast<SecretItem*>(first->data);
  auto created = base::Time::FromTimeT(
      LibsecretLoader::secret_item_get_created(secret_item));
  auto last_modified = base::Time::FromTimeT(
      LibsecretLoader::secret_item_get_modified(secret_item));

  VLOG(1) << "Libsecret key created: " << created;
  VLOG(1) << "Libsecret key last modified: " << last_modified;
  LOG_IF(WARNING, created != last_modified)
      << "the encryption key has been modified since it was created.";
}

}
 ... 
```
### patch
```cpp
#include "base/command_line.h"

namespace {
const char* GetApplicationName();
}  // namespace
namespace {

const char* GetApplicationName() {
  base::CommandLine* command_line = base::CommandLine::ForCurrentProcess();
  if (command_line->HasSwitch("import-chrome")) {
    return "chrome";
  } else if (command_line->HasSwitch("import-chromium") ||
             command_line->HasSwitch("import-brave")) {
    return "chromium";
  } else {
    return "brave";
  }
}

}  // namespace

```

