### match
```
...
 # ifndef ... 
 namespace blink { ... 
static void ParseDocumentFragment(
      const String&,
      DocumentFragment*,
      Element* context_element,
      CustomElementRegistry*,
      ParserContentPolicy = kAllowScriptingContent);
 // Exposed for testing. 
 >>> 
HTMLParserScriptRunnerHost* AsHTMLParserScriptRunnerHostForTesting() {
    return this;
  }
 ... } ...  
```
### patch
```
  IF_BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH, void HTMLDocumentParserConstructed();)

```

### match
```
...
 # ifndef ... 
;
 } 
 // namespace blink 
 >>> 
 ... 
```
### patch
```
#if BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)
namespace cppgc {
template <typename T, typename>
struct PostConstructionCallbackTrait;

// This PostConstruction extension adds
// HTMLDocumentParser::HTMLDocumentParserConstructed() call after the
// HTMLDocumentParser construction. We use this to disable HTMLResourcePreloader
// when a PageGraph session is active, which allows us to connect network
// requests with the actual DOM Nodes.

template <typename T>
struct PostConstructionCallbackTrait<
    T,
    typename std::enable_if<
        std::is_base_of<blink::HTMLDocumentParser, T>::value,
        void>::type> {
  static void Call(blink::HTMLDocumentParser* object) {
    object->HTMLDocumentParserConstructed();
  }
};

}  // namespace cppgc
#endif  // BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)

```

