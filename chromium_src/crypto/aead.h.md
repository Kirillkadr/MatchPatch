### match
```cpp
...
 
 # ifndef ... 
 
 namespace crypto { ... 
 
 class CRYPTO_EXPORT Aead { ... 
bool Open(std::string_view ciphertext,
            std::string_view nonce,
            std::string_view additional_data,
            std::string* plaintext) const;
 size_t KeyLength() const; 
 >>> 
size_t NonceLength() const;
 ... } ...  } ...  
```
### patch
```cpp
  size_t OverrideNonceLength(size_t length) { 
    nonce_length_ = length;
    return length;
  }

 private:
  size_t nonce_length_ = 0;

 public:

```

