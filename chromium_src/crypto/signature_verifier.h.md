### match
```cpp
...
 
 # ifndef ... 
 
 namespace crypto { ... 
 
 class CRYPTO_EXPORT SignatureVerifier { ...   >>> 
 ECDSA_SHA256 
 ,  <<< 
// This is RSA-PSS with SHA-256 as both signing hash and MGF-1 hash, and the
 ... } ...  } ...  
```
### patch
```cpp
    ECDSA_SHA256, ECDSA_SHA384,

```

