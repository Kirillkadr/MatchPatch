### match
```cpp
...
 
 # ifndef ... 
 
 namespace web { ... 
// By default, "object-src 'none';" is added to CSP. Override to change this.
 virtual std::string GetContentSecurityPolicyObjectSrc() const; 
 >>> 
// By default, the "X-Frame-Options: DENY" header is sent. To stop this from
 ... } ...  
```
### patch
```cpp
  virtual std::string GetContentSecurityPolicyFrameSrc() const;

```

