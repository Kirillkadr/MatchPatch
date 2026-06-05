### match
```cpp
...
 
 namespace extensions { ... 
 
 class ChromePermissionMessageRule { ... 
// Returns all the rules used to generate permission messages for Chrome apps
 // and extensions. 
 >>> 
static std::vector<ChromePermissionMessageRule> GetAllRules();
 ... } ...  } ...  
```
### patch
```cpp
  static std::vector<ChromePermissionMessageRule> GetAllRules_ChromiumImpl(); 

```

