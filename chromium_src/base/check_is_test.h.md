### match
```
...
#define CHECK_IS_NOT_TEST(...) \
  CHECK(!base::internal::get_is_test_impl(), __VA_ARGS__)

 #endif 
 // BASE_CHECK_IS_TEST_H_ 
 >>> 
 ... 
```
### patch
```

namespace variations {
class PublicKeyWrapper;
}

namespace base {

enum class TestVendor { kNone, kChromium, kBrave };

// Returns currently running test vendor. Private interface to allow-list usage.
class BASE_EXPORT CurrentTestVendor {
 private:
  FRIEND_TEST_ALL_PREFIXES(CurrentTestVendorTest, IsBrave);
  friend variations::PublicKeyWrapper;
  static TestVendor Get();
};

}  // namespace base
```

