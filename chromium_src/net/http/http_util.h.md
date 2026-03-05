### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT HttpUtil { ... 
// values, which may contain a comma (see RFC 2616 section 3.3.1).
 static bool IsNonCoalescingHeader(std::string_view name); 
 >>> 
// Return true if the character is HTTP "linear white space" (SP | HT).
 ... } ...  } ...  
```
### patch
```
  static bool IsNonCoalescingHeader_ChromiumImpl(std::string_view name);

```

