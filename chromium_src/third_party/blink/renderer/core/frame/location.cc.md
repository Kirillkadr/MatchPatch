### match
```
...
 namespace blink { ...   >>> 
 DOMStringList 
 * Location::ancestorOrigins() const 
 {  <<< ... 
auto* origins = MakeGarbageCollected<DOMStringList>();
 ... } ...  } ...  
```
### patch
```
DOMStringList* Location::ancestorOrigins_ChromiumImpl() const {

```

### match
```
...
 namespace blink { ... 
 bool Location::IsAttached() const { ... 
return dom_window_->GetFrame();
 } 
 >>> 
 ... } ...  
```
### patch
```
DOMStringList* Location::ancestorOrigins() const {
  auto* raw_origins = ancestorOrigins_ChromiumImpl();
  if (!IsAttached() || !raw_origins || raw_origins->IsEmpty()) {
    return raw_origins;
  }
  auto* filtered_origins = MakeGarbageCollected<DOMStringList>();
  const auto* innermost_origin =
      DomWindow()->GetFrame()->GetSecurityContext()->GetSecurityOrigin();

  auto is_onion_service = [](const SecurityOrigin* origin) {
    return origin->Host().EndsWith(".onion", kTextCaseASCIIInsensitive);
  };

  auto is_chrome_untrusted = [](const SecurityOrigin* origin) {
    return origin->Protocol() == "chrome-untrusted";
  };

  for (uint32_t i = 0; i < raw_origins->length(); ++i) {
    const String raw_origin = raw_origins->item(i);
    const scoped_refptr<SecurityOrigin> origin =
        SecurityOrigin::CreateFromString(raw_origin);
    if (is_chrome_untrusted(origin.get())) {
      break;
    }
    if (is_onion_service(origin.get()) &&
        !origin->IsSameOriginWith(innermost_origin)) {
      filtered_origins->Append("\"null\"");
    } else {
      filtered_origins->Append(raw_origin);
    }
  }

  return filtered_origins;
}

```

