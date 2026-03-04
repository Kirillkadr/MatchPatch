### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
 
 class CookiesEventRouter : public ProfileObserver { ... 
~CookiesEventRouter() override;
 // ProfileObserver: 
 >>> 
void OnOffTheRecordProfileCreated(Profile* off_the_record) override;
 ... } ...  } ...  
```
### patch
```
  void OnOffTheRecordProfileCreated_ChromiumImpl(Profile* off_the_record);

```

### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
class CookieChangeListener : public network::mojom::CookieChangeListener {
   public:
    CookieChangeListener(CookiesEventRouter* router, bool otr);

    CookieChangeListener(const CookieChangeListener&) = delete;
    CookieChangeListener& operator=(const CookieChangeListener&) = delete;

    ~CookieChangeListener() override;

    // network::mojom::CookieChangeListener:
    void OnCookieChange(const net::CookieChangeInfo& change) override;

   private:
    raw_ptr<CookiesEventRouter> router_;
    bool otr_;
  };
 void MaybeStartListening(); 
 >>> 
void BindToCookieManager(
      mojo::Receiver<network::mojom::CookieChangeListener>* receiver,
      Profile* profile);
 ... } ...  
```
### patch
```
  friend struct OnCookieChangeExposeForTesting;


```

### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
 
 class CookiesAPI : public BrowserContextKeyedAPI, public EventRouter::Observer { ... 
std::unique_ptr<CookiesEventRouter> cookies_event_router_;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```
struct OnCookieChangeExposeForTesting {
  static void CallOnCookieChangeForOtr(CookiesAPI* cookies_api);
};


```

