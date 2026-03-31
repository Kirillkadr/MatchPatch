### match
```cpp
...
 
 namespace policy { ... 
std::vector<std::unique_ptr<policy::ConfigurationPolicyProvider>>  >>> 
 ChromeBrowserPolicyConnector::CreatePolicyProviders() 
 { 
 auto providers = BrowserPolicyConnector::CreatePolicyProviders();  <<< 
std::unique_ptr<ConfigurationPolicyProvider> platform_provider =
      CreatePlatformProvider();
 ... } ...  } ...  
```
### patch
```cpp
ChromeBrowserPolicyConnector::CreatePolicyProviders_ChromiumImpl() {
  auto providers = BrowserPolicyConnector::CreatePolicyProviders_ChromiumImpl();

```

