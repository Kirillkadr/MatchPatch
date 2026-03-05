### match
```
...
 NET_EXPORT ProxyServer ProxyUriToProxyServer(std::string_view uri,
                                             ProxyServer::Scheme default_scheme,
                                             bool is_quic_allowed = false);
 >>>  ...
```
### patch
```
NET_EXPORT std::string ProxyServerToProxyUri_ChromiumImpl(const ProxyServer& proxy_server); 

```

