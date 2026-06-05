### match
```cpp
...
 
 namespace regional_capabilities { ... 
 
 country_codes::CountryId CountryIdHolder::GetForTesting() const { ... 
return country_id_;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
country_codes::CountryId CountryIdHolder::GetCountryCode() const {
  return country_id_;
}

```

