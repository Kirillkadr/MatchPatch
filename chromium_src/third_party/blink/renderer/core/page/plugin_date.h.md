### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT PluginInfo final : public GarbageCollected<PluginInfo> { ... 
 bool may_use_mime_handler_view 
 ) 
 ; 
 >>> 
void AddMimeType(MimeClassInfo*);
 ... } ...  } ...  
```
### patch
```
  void SetName(const String& new_name) { name_ = new_name; }
  void SetFilename(const String& new_filename) { filename_ = new_filename; }

```

