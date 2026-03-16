### match
```
...
 
 net::NetworkTrafficAnnotationTag
GdpServiceHandler::NetworkTrafficAnnotationTag() const { ... 
return kGdpTrafficAnnotation;
 } 
 >>> 
 ... 
```
### patch
```

// Override to disable GDP service handler requests as it sends them to
// googleapis.com.
void GdpServiceHandler::CanMakeRequest(
    Profile* profile,
    base::OnceCallback<void(bool success)> callback) {
  std::move(callback).Run(false);
}

```

