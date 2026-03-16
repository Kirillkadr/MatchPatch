### match
```
...
 
 # ifndef ... 
 
 class GdpServiceHandler : public DevToolsHttpServiceHandler { ... 
 // DevToolsHttpServiceHandler overrides: 
 >>> 
GURL BaseURL() const override;
 ... } ...  
```
### patch
```
  void CanMakeRequest(Profile* profile,
                      base::OnceCallback<void(bool success)> callback) override;

```

