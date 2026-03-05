### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT SVGResourceDocumentContent final
    : public GarbageCollected<SVGResourceDocumentContent> { ... 
void ContentChanged();
 void LoadingFinished(); 
 >>> 
void AsyncLoadingFinished();
 ... } ...  } ...  
```
### patch
```
#if BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)
  void AsyncLoadingFinished();
 public:
  blink::DOMNodeId initiator_dom_node_id() const {
    return initiator_dom_node_id_;
  }
  blink::DOMNodeId set_initiator_dom_node_id(blink::DOMNodeId dom_node_id) {
    return initiator_dom_node_id_ = dom_node_id;
  }

 private:
  blink::DOMNodeId initiator_dom_node_id_ = blink::kInvalidDOMNodeId
#endif  // BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)


```

