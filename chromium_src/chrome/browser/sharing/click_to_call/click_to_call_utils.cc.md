### match
```cpp
...
>>>
 bool 
 ShouldOfferClickToCallForURL 
 ( 
 content::BrowserContext* browser_context 
 ,  <<< 
const GURL& url
 ... ) ...  
```
### patch
```cpp
bool ShouldOfferClickToCallForURL_ChromiumImpl(content::BrowserContext* browser_context,

```

### match
```cpp
...
 
 bool IsUrlSafeForClickToCall(const GURL& url) { ... 
return !unescaped.empty() && std::ranges::none_of(unescaped, [](char c) {
    return c == '#' || c == '*' || c == '%';
  });
 } 
 >>> 
 ... 
```
### patch
```cpp
bool ShouldOfferClickToCallForURL(content::BrowserContext* browser_context,
                                  const GURL& url) {
  return false;
}
```

