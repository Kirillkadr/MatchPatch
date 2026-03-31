### match
```cpp
...
 
 namespace regional_capabilities { ...   >>> 
 RegionalCapabilitiesServiceClientLinux::RegionalCapabilitiesServiceClientLinux 
 (  <<< 
variations::VariationsService* variations_service
 ... ) ...  } ...  
```
### patch
```cpp
RegionalCapabilitiesServiceClientLinux_ChromiumImpl::RegionalCapabilitiesServiceClientLinux_ChromiumImpl(

```

### match
```cpp
...
 
 namespace regional_capabilities { ... 
RegionalCapabilitiesServiceClientLinux_ChromiumImpl::RegionalCapabilitiesServiceClientLinux_ChromiumImpl(
	variations::VariationsService* variations_service)
    : RegionalCapabilitiesServiceClient(variations_service),
      variations_permanent_country_id_(
          variations_service
              ? CountryId(base::ToUpperASCII(
                    variations_service->GetStoredPermanentCountry()))
              : CountryId()) {}  >>> 
 RegionalCapabilitiesServiceClientLinux::
    ~RegionalCapabilitiesServiceClientLinux() = default;  <<< 
void RegionalCapabilitiesServiceClientLinux::FetchCountryId(
    CountryIdCallback on_country_id_fetched) {
  std::move(on_country_id_fetched).Run(variations_permanent_country_id_);
}
 ... } ...  
```
### patch
```cpp
RegionalCapabilitiesServiceClientLinux_ChromiumImpl::
    ~RegionalCapabilitiesServiceClientLinux_ChromiumImpl() = default;

```

### match
```cpp
...
 
 namespace regional_capabilities { ...   >>> 
 void 
 RegionalCapabilitiesServiceClientLinux::FetchCountryId 
 (  <<< 
CountryIdCallback on_country_id_fetched
 ... ) ...  } ...  
```
### patch
```cpp

void RegionalCapabilitiesServiceClientLinux_ChromiumImpl::FetchCountryId(

```

### match
```cpp
...
 
 namespace regional_capabilities { ... 
 
 void RegionalCapabilitiesServiceClientLinux_ChromiumImpl::FetchCountryId(
	CountryIdCallback on_country_id_fetched) { ... 
std::move(on_country_id_fetched).Run(variations_permanent_country_id_);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
RegionalCapabilitiesServiceClientLinux::
    ~RegionalCapabilitiesServiceClientLinux() = default;

void RegionalCapabilitiesServiceClientLinux::FetchCountryId(
    CountryIdCallback country_id_fetched_callback) {
  // Fall back onto the platform neutral implementation that uses device locale.
  return RegionalCapabilitiesServiceClient::FetchCountryId(
      std::move(country_id_fetched_callback));
}


```

