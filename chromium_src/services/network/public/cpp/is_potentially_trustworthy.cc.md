### match
```
...   >>> 
 if 
 (net::IsLocalhost(origin.GetURL()))  <<< ...
```
### patch
```
  if (net::IsLocalhostOrOnion(origin.GetURL()))

```

