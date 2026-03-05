### match
```
...
 # ifndef ... 
 namespace blink { ... 
SubresourceFilter* GetSubresourceFilter() const override;  >>> 
 bool AllowScript() const override;  <<< ... 
bool ShouldBlockRequestByInspector(const KURL&) const override;
 ... } ...  
```
### patch
```
  bool AllowScript_Unused() const; 
  bool AllowScript(const KURL& url) const override;

```

