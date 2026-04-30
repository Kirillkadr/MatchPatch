### match
```cpp
...
 
 namespace crypto { ... 
 size_t 
 Aead::NonceLength() const 
 { 
 >>> 
return aead::NonceSizeFor(algorithm_);
 ... } ...  } ...  
```
### patch
```cpp
if (nonce_length_)       
    return nonce_length_;

```

