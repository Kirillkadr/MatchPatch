### match
```
...
 namespace blink { ... 
  >>>  } ...
```
### patch
```
#if BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)
void HTMLDocumentParser::HTMLDocumentParserConstructed() {
  if (CoreProbeSink::HasAgentsGlobal(CoreProbeSink::kPageGraph)) {
    // Fully disable preloader if a PageGraph session is active.
    preloader_ = nullptr;
  }
}
#endif  // BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)

```