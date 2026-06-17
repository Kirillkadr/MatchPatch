### match
```cpp
...
 
 namespace variations { ... 
 
 void VariationsService::OnSimpleLoaderComplete(
    std::optional<std::string> response_body) { ... 
 std::optional<base::Time> response_date = headers->GetDateValue(); 
 >>> 
// If the seed was fetched securely, opportunistically update the network time
 ... } ...  } ...  
```
### patch
```cpp
  if (response_code == net::HTTP_NOT_MODIFIED && is_first_request) {
    std::string_view country_code =
        GetHeaderValue(headers.get(), "X-Country");
    if (!country_code.empty()) {
      local_state_->SetString(prefs::kVariationsCountry, country_code);
    }                                                                   
  };

```

