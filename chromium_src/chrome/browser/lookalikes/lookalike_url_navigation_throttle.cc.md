### match
```
...
>>>
 void 
 LookalikeUrlNavigationThrottle::MaybeCreateAndAdd 
 (  <<< 
content::NavigationThrottleRegistry& registry
 ... ) ...  
```
### patch
```
void LookalikeUrlNavigationThrottle::MaybeCreateAndAdd_ChromiumImpl(

```

### match
```
...
 
 ThrottleCheckResult LookalikeUrlNavigationThrottle::PerformChecks(
    const std::vector<DomainInfo>& engaged_sites) { ... 
return NavigationThrottle::PROCEED;
 } 
 >>> 
 ... 
```
### patch
```

void LookalikeUrlNavigationThrottle::MaybeCreateAndAdd(
    content::NavigationThrottleRegistry& registry) {}
```

