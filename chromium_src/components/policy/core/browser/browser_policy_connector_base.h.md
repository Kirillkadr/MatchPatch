### match
```cpp
...
 
 # ifndef ... 
 
 namespace policy { ... 
std::vector<std::unique_ptr<ConfigurationPolicyProvider>>
 CreatePolicyProviders() 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
  std::vector<std::unique_ptr<ConfigurationPolicyProvider>>
      CreatePolicyProviders_ChromiumImpl();

```

