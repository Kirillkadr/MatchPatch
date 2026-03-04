### match
```
...
#include "build/build_config.h"

 #include "base/strings/string_view_rust.h"
 
 >>> 
#include "third_party/rust/serde_json_lenient/v0_2/wrapper/functions.h"

 ... 
```
### patch
```
#include "base/notimplemented.h"

```

### match
```
...
 namespace serde_json_lenient { ... 
 >>> 
 } ...  
```
### patch
```
// TODO(https://github.com/brave/brave-browser/issues/47120): These methods are
// not implemented for now, but their purpose is to eventually hook up the
// the `serde_json_lenient` to `base::Value`, and let us store binary blobs
// whenever dealing with 64bit integers that cannot be represented in
// `base::Value`.

void list_append_i64(base::ListValue& ctx, int64_t val) {
  NOTIMPLEMENTED();
}

void list_append_u64(base::ListValue& ctx, uint64_t val) {
  NOTIMPLEMENTED();
}

void dict_set_i64(base::DictValue& ctx, rust::Str key, int64_t val) {
  NOTIMPLEMENTED();
}

void dict_set_u64(base::DictValue& ctx, rust::Str key, uint64_t val) {
  NOTIMPLEMENTED();
}

```

