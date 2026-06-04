### match
```cpp
...
 >>> 
int extra_info_spec = 0;
  RawListeners listeners = GetMatchingListeners(
      browser_context, keys::kOnAuthRequiredEvent, request, &extra_info_spec);
  if (listeners.empty()) {
    return AuthRequiredResponse::AUTH_REQUIRED_RESPONSE_NO_ACTION;
```
### patch
```cpp
if (browser_context) {                                                     
    ClearSignaled(browser_context, request->id,                              
                  EventTypes::kOnBeforeSendHeaders);                         
    ClearSignaled(browser_context, request->id, EventTypes::kOnSendHeaders); 
    ClearSignaled(browser_context, request->id,                              
                  EventTypes::kOnHeadersReceived);                           
  }

```
