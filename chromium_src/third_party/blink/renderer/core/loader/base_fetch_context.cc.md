### match
```
...
 namespace blink { ... 
 std::optional<ResourceRequestBlockedReason>
BaseFetchContext::CanRequestInternal(
    ResourceType type,
    const ResourceRequest& resource_request,
    const KURL& url,
    const ResourceLoaderOptions& options,
    ReportingDisposition reporting_disposition,
    base::optional_ref<const ResourceRequest::RedirectInfo> redirect_info)
    const { ...   >>> 
 if 
 (!AllowScript()) 
 {  <<< ... 
// TODO(estark): Use a different ResourceRequestBlockedReason here, since
 ... } ...  } ...  } ...  
```
### patch
```
    if (!AllowScript(url)) {

```

