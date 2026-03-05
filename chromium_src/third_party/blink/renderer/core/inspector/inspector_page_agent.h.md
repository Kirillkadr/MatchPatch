### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT InspectorPageAgent final
    : public InspectorBaseAgent<protocol::Page::Metainfo> { ... 
 const protocol::Binary& data 
 ) 
 override 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```
  protocol::Response NotUsed();                                                                   \
  protocol::Response generatePageGraph(String* data) override;                 \
  protocol::Response generatePageGraphNodeReport(                              \
      int node_id, std::unique_ptr<protocol::Array<String>>* report) override; \

```

