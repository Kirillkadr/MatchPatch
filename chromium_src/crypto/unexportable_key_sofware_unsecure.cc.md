### match
```cpp
...
 
 namespace { ... 
 
 class SoftwareProvider : public UnexportableKeyProvider { ... 
 
 std::optional<SignatureVerifier::SignatureAlgorithm> SelectAlgorithm(
      base::span<const SignatureVerifier::SignatureAlgorithm>
          acceptable_algorithms) override { ...   >>> 
 case 
 SignatureVerifier::SignatureAlgorithm::RSA_PSS_SHA256 
 :  <<< 
continue;
 ... } ...  } ...  } ...  
```
### patch
```cpp
        case SignatureVerifier::SignatureAlgorithm::RSA_PSS_SHA256:      \
  case SignatureVerifier::SignatureAlgorithm::ECDSA_SHA384:

```

### match
```cpp
...
 
 namespace { ... 
 
 class SoftwareProvider : public UnexportableKeyProvider { ... 
 
 std::unique_ptr<UnexportableSigningKey> GenerateSigningKeySlowly(
      base::span<const SignatureVerifier::SignatureAlgorithm>
          acceptable_algorithms) override { ... 
 case 
 SignatureVerifier::SignatureAlgorithm::RSA_PSS_SHA256 
 : 
 >>> 
continue;
 ... } ...  } ...  } ...  
```
### patch
```cpp
  case SignatureVerifier::SignatureAlgorithm::ECDSA_SHA384:

```

