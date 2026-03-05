### match
```
...
 namespace blink { ... 
 bool FetchContext::StartSpeculativeImageDecode(Resource* resource) { ... 
return false;
 } 
 >>> 
 ... } ...  
```
### patch
```
String FetchContext::GetCacheIdentifierIfCrossSiteSubframe() const {
  return String();
}

```

