### match
```cpp
...
  SEQUENCE_CHECKER(sequence_checker_);
  base::WeakPtrFactory<WalletHttpClientImpl> weak_ptr_factory_{this};

 } 
 ; 
 >>> 
 ...
```
### patch
```cpp
WalletHttpClientImpl::WalletHttpClientImpl(
    signin::IdentityManager* identity_manager,
    scoped_refptr<network::SharedURLLoaderFactory> url_loader_factory) {}
WalletHttpClientImpl::~WalletHttpClientImpl() = default;

void WalletHttpClientImpl::SavePass(const WalletablePass& pass,
                                    SavePassCallback callback) {
  std::move(callback).Run(
      base::unexpected(WalletHttpClient::WalletRequestError::kGenericError));
}

```

