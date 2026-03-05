### match
```
...
 namespace blink { ... 
 void HTMLMetaElement::ProcessMetaCH(Document& document,
                                    const AtomicString& content,
                                    network::MetaCHType type,
                                    bool is_doc_preloader,
                                    bool is_sync_parser) { ...   >>> 
 if 
 (!frame->ScriptEnabled()) 
 {  <<< ... 
// Do not allow configuring client hints if JavaScript is disabled.
 ... } ...  } ...  } ...  
```
### patch
```
  if (!frame->ScriptEnabled(document.Url())) {

```

