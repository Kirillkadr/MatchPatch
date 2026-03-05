### match
```
...
 EVENT_TYPE(PROXY_RESOLUTION_OVERRIDE_RULE_APPLIED) 
 >>> 
 ... 
```
### patch
```

// Intentionally no header guards (see the comment in the overridden .h file).
// NOLINT(build/header_guard)
// no-include-guard-because-multiply-included
// The time spent sending authentication to the SOCKS server
EVENT_TYPE(SOCKS5_AUTH_WRITE)

// The time spent waiting for the authentication response from the SOCKS server
EVENT_TYPE(SOCKS5_AUTH_READ)
```

