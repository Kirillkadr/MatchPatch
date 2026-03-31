### match
```cpp
...
 std::unique_ptr<KeyedService>
  >>> 
 GAIAInfoUpdateServiceFactory::BuildServiceInstanceForBrowserContext 
 (  <<< 
content::BrowserContext* context
 ... ) ...  
```
### patch
```cpp
GAIAInfoUpdateServiceFactory::BuildServiceInstanceForBrowserContext_ChromiumImpl(

```

### match
```cpp
...
 
 bool GAIAInfoUpdateServiceFactory::ServiceIsCreatedWithBrowserContext() const { ... 
return true;
 } 
 >>> 
 ... 
```
### patch
```cpp
std::unique_ptr<KeyedService>
GAIAInfoUpdateServiceFactory::BuildServiceInstanceForBrowserContext(
    content::BrowserContext* context) const {
  return nullptr;
}
```

