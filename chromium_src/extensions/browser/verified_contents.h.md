### match
```cpp
...
 
 # ifndef ... 
 
 namespace extensions { ... 
 
 class VerifiedContents { ... 
// validating the enclosed signature. Returns nullptr on failure. Note:
 // `public_key` must remain valid for the lifetime of the returned object. 
 >>> 
static std::unique_ptr<VerifiedContents> Create(
      base::span<const uint8_t> public_key,
      std::string_view contents);
 ... } ...  } ...  
```
### patch
```cpp
  static std::unique_ptr<VerifiedContents> Create_ChromiumImpl(VerifiedContents* vc, std::string_view contents); \

```

