### match
```
...
 # ifndef ... 
 namespace 
 blink 
 { 
 >>> 
class ContainerNode
 ... } ...  
```
### patch
```
#if BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)
class ActiveScriptWrappableBase;
#endif  // BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT Node : public EventTarget { ... 
 void ClearChildNeedsStyleInvalidation() { ... 
ClearFlag(kChildNeedsStyleInvalidationFlag);
 } 
 >>> 
 ... } ...  } ...  
```
### patch
```
  IF_BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH, void NodeConstructed();)

```

### match
```
...
 # ifndef ... 
 namespace cppgc { ... 
 struct SpaceTrait<T> { ... 
using Space = blink::NodeSpace;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```
#if BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)
template <typename T, typename>
struct PostConstructionCallbackTrait;

// This PostConstruction extension adds Node::NodeConstructed() call after the
// Node construction. We use this to track fully constructed Node in the
// PageGraph engine. It's important to have all subclasses constructed so we can
// get the actual Node type and do DynamicTo<>() conversion if required.
template <typename T>
struct PostConstructionCallbackTrait<
    T,
    typename std::enable_if<
        std::is_base_of<blink::Node, T>::value &&
            !HasActiveScriptWrappableBaseConstructed<T>::value,
        void>::type> {
  static void Call(blink::Node* object) { object->NodeConstructed(); }
};

// If Node is derived from ActiveScriptWrappable<> we need to call both
// PostConstructionCallbacks.
template <typename T>
struct PostConstructionCallbackTrait<
    T,
    typename std::enable_if<
        std::is_base_of<blink::Node, T>::value &&
            HasActiveScriptWrappableBaseConstructed<T>::value,
        void>::type> {
  template <typename U>
  struct class_of {};

  template <typename U, typename R>
  struct class_of<R(U::*)> {
    using type = U;
  };

  static void Call(T* object) {
    // Ensure we use a proper ActiveScriptWrappable<> post construction trait.
    using ActiveScriptWrappableType = typename class_of<
        decltype(&T::ActiveScriptWrappableBaseConstructed)>::type;
    static_assert(
        std::is_base_of<blink::ActiveScriptWrappableBase,
                        ActiveScriptWrappableType>::value &&
        !std::is_base_of<blink::Node, ActiveScriptWrappableType>::value);
    PostConstructionCallbackTrait<ActiveScriptWrappableType>::Call(object);

    PostConstructionCallbackTrait<blink::Node>::Call(object);
  }
};
#endif  // BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)

```

