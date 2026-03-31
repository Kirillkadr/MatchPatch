### match
```cpp
...
 
 # ifndef ... 
 
 namespace regional_capabilities { ...   >>> 
 class 
 RegionalCapabilitiesServiceClientLinux  <<< 
: public RegionalCapabilitiesServiceClient
 ... } ...  
```
### patch
```cpp
class RegionalCapabilitiesServiceClientLinux_ChromiumImpl

```

### match
```cpp
...
class RegionalCapabilitiesServiceClientLinux_ChromiumImpl  >>> 
 public 
 RegionalCapabilitiesServiceClient 
 {  <<< 
public:
  explicit RegionalCapabilitiesServiceClientLinux(
      variations::VariationsService* variations_service);
 ... } ...  
```
### patch
```cpp
    : public RegionalCapabilitiesServiceClient {

```

### match
```cpp
...
 
 class RegionalCapabilitiesServiceClientLinux_ChromiumImpl
	     : public RegionalCapabilitiesServiceClient { ...   >>> 
 explicit 
 RegionalCapabilitiesServiceClientLinux 
 (  <<< 
variations::VariationsService* variations_service
 ... ) ...  } ...  
```
### patch
```cpp
  explicit RegionalCapabilitiesServiceClientLinux_ChromiumImpl(

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace regional_capabilities { ... 
 
 class RegionalCapabilitiesServiceClientLinux_ChromiumImpl
	     : public RegionalCapabilitiesServiceClient { ... 
explicit RegionalCapabilitiesServiceClientLinux_ChromiumImpl(
		variations::VariationsService* variations_service);  >>> 
 ~RegionalCapabilitiesServiceClientLinux() override;  <<< 
void FetchCountryId(CountryIdCallback country_id_fetched_callback) override;
 ... } ...  } ...  
```
### patch
```cpp
  ~RegionalCapabilitiesServiceClientLinux_ChromiumImpl() override;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace regional_capabilities { ... 
 
 class RegionalCapabilitiesServiceClientLinux_ChromiumImpl
	     : public RegionalCapabilitiesServiceClient { ... 
const country_codes::CountryId variations_permanent_country_id_;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
class RegionalCapabilitiesServiceClientLinux
    : public RegionalCapabilitiesServiceClientLinux_ChromiumImpl {
 public:
  using RegionalCapabilitiesServiceClientLinux_ChromiumImpl::
      RegionalCapabilitiesServiceClientLinux_ChromiumImpl;
  ~RegionalCapabilitiesServiceClientLinux() override;

  void FetchCountryId(CountryIdCallback country_id_fetched_callback) override;
};


```

