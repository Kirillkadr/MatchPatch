### match
```cpp
...
 
 namespace content { ... 
 
 namespace signed_exchange_utils { ...   >>> 
 bool 
 IsSignedExchangeReportingForDistributorsEnabled() 
 {  <<< 
return base::FeatureList::IsEnabled(network::features::kReporting);
 ... } ...  } ...  } ...  
```
### patch
```cpp
bool IsSignedExchangeReportingForDistributorsEnabled_Chromium() {

```

### match
```cpp
...
 
 namespace content { ... 
 
 namespace signed_exchange_utils { ... 
 
 bool IsCookielessOnlyExchange(const net::HttpResponseHeaders& inner_headers) { ... 
return false;
 } 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
bool IsSignedExchangeReportingForDistributorsEnabled_Chromium() {
  return false;
}

```

