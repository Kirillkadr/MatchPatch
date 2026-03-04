### match
```
...
 namespace { ... 
 bool g_this_is_a_test = false; 
 >>> 
 ... } ...  
```
### patch
```
bool g_this_is_a_brave_test = false;

```

### match
```
...
 namespace base::test { ... 
 BASE_EXPORT void AllowCheckIsTestForTesting() { ... 
 g_this_is_a_test = true; 
 >>> 
 ... } ...  } ...  
```
### patch
```
  BASE_EXPORT void SetTestVendorIsBraveForTesting() {
  g_this_is_a_brave_test = true;
}

```

### match
```
...
 namespace base::test { ... 
BASE_EXPORT void AllowCheckIsTestForTesting() {
  g_this_is_a_test = true;
  BASE_EXPORT void SetTestVendorIsBraveForTesting() {
		  g_this_is_a_brave_test = true;
		}
		}
 } 
 // namespace base::test 
 >>> 
 ... 
```
### patch
```

namespace base {

// static
TestVendor CurrentTestVendor::Get() {
  if (g_this_is_a_brave_test) {
    return TestVendor::kBrave;
  }
  if (g_this_is_a_test) {
    return TestVendor::kChromium;
  }
  return TestVendor::kNone;
}

}  // namespace base
```

