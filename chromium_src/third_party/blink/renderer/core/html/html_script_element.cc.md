### match
```
...
 namespace blink { ... 
 void HTMLScriptElement::Trace(Visitor* visitor) const { ... 
ScriptElementBase::Trace(visitor);
 } 
 >>> 
 ... } ...  
```
### patch
```
// static
bool HTMLScriptElement::supports(const AtomicString& type) {
  if (type == script_type_names::kWebbundle)
    return false;
  // There used to be a kSpeculationRulesPrefetchProxy feature flag to disable
  // speculative prefetching in the upstream function, but with its removal, it
  // was necessary to move the check here.
  if (type == script_type_names::kSpeculationrules) {
    return false;
  }

  return supports_ChromiumImpl(type);
}

```

