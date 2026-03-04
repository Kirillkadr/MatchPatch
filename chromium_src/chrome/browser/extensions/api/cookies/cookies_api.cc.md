### match
```
...
 
 namespace extensions { ... 
 
 void CookiesEventRouter::OnCookieChange(bool otr,
                                        const net::CookieChangeInfo& change) { ... 
 if ( ...   >>> 
 !change.cookie.PartitionKey()->IsSerializeable() 
 ) 
 {  <<< 
return;
 ... } ...  } ...  } ...  
```
### patch
```
      !change.cookie.PartitionKey()->IsSerializeable() ||
      (otr && !profile_->GetPrimaryOTRProfile(/*create_if_needed=*/false))) {

```

### match
```
...
 
 namespace extensions { ...   >>> 
 void 
 CookiesEventRouter::OnOffTheRecordProfileCreated(Profile* off_the_record) 
 {  <<< 
// When an off-the-record spinoff of |profile_| is created, start listening
 ... } ...  } ...  
```
### patch
```
void CookiesEventRouter::OnOffTheRecordProfileCreated_ChromiumImpl(Profile* off_the_record) {

```

### match
```
...
 
 namespace extensions { ... 
 
 void CookiesAPI::OnListenerAdded(const EventListenerInfo& details) { ... 
EventRouter::Get(browser_context_)->UnregisterObserver(this);
 } 
 >>> 
 ... } ...  
```
### patch
```
// static
void OnCookieChangeExposeForTesting::CallOnCookieChangeForOtr(
    CookiesAPI* cookies_api) {
  cookies_api->cookies_event_router_->OnCookieChange(true,
                                                     net::CookieChangeInfo());
}

void CookiesEventRouter::OnOffTheRecordProfileCreated(Profile* off_the_record) {
  if (off_the_record->IsTor()) {
    return;
  }

  OnOffTheRecordProfileCreated_ChromiumImpl(off_the_record);
}


```

