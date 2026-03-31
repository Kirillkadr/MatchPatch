### match
```cpp
...
 
 # ifndef ... 
 
 namespace crypto::obsolete { ... 
 
 class CRYPTO_EXPORT Md5 { ...   >>> 
 FRIEND_TEST_ALL_PREFIXES(Md5Test, KnownAnswer);  <<<  ...} ...  } ...  
```
### patch
```cpp
  FRIEND_TEST_ALL_PREFIXES(Md5Test, KnownAnswer); friend std::array<uint8_t, crypto::obsolete::kMd5Size> 
  brave::Md5ForDefaultProtocolHandler(base::span<const uint8_t> data);

```

