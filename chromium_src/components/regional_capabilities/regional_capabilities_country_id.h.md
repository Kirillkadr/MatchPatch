### match
```cpp
...
 
 namespace regional_capabilities { ... 
 
 class CountryIdHolder final { ... 
bool operator==(const CountryIdHolder& other) const;
 // Returns the wrapped country ID, usable in test code only. 
 >>> 
country_codes::CountryId GetForTesting() const;
 ... } ...  } ...  
```
### patch
```cpp
  country_codes::CountryId GetCountryCode() const; 

```

