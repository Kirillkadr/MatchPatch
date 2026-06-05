### match
```cpp
...
 
 class MutableProfileOAuth2TokenServiceDelegate
    : public ProfileOAuth2TokenServiceDelegate,
      public WebDataServiceConsumer,
      public network::NetworkConnectionTracker::NetworkConnectionObserver { ... 
void RevokeCredentialsOnServer(const std::string& refresh_token);
 // Starts a fetch for wrapped keys from the web database. 
 >>> 
void StartWebWrappedKeyFetch();
 ... } ...  
```
### patch
```cpp
  friend class BraveMutableProfileOAuth2TokenServiceDelegate; 

```

