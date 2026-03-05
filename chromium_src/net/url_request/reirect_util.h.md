### match
```
...
 # ifndef ... 
 namespace net { ... 
 class RedirectUtil { ... 
// |should_clear_upload| is set to true when the request body should be
 // cleared during the redirect. 
 >>> 
NET_EXPORT static void UpdateHttpRequest(
      const GURL& original_url,
      std::string_view original_method,
      const RedirectInfo& redirect_info,
      const std::optional<std::vector<std::string>>& removed_headers,
      const std::optional<net::HttpRequestHeaders>& modified_headers,
      HttpRequestHeaders* request_headers,
      bool* should_clear_upload);
 ... } ...  } ...  
```
### patch
```
  NET_EXPORT static void UpdateHttpRequest_ChromiumImpl(
      const GURL& original_url, std::string_view original_method,
      const RedirectInfo& redirect_info,
      const std::optional<std::vector<std::string>>& removed_headers,
      const std::optional<net::HttpRequestHeaders>& modified_headers,
      HttpRequestHeaders* request_headers, bool* should_clear_upload);

```

