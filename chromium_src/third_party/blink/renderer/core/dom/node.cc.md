### match
```
...
 namespace blink { ... 
 void Node::Trace(Visitor* visitor) const { ... 
EventTarget::Trace(visitor);
 } 
 >>> 
 ... } ...  
```
### patch
```
#if BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)
void Node::NodeConstructed() {
  // Document is required for probe sink.
  if (tree_scope_)
    probe::RegisterPageGraphNodeFullyCreated(this);
}
#endif  // BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)



```

