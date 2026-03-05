### match
```
...
 namespace blink { ... 
 void LinkLoader::LoadStylesheet(
    const LinkLoadParameters& params,
    const AtomicString& local_name,
    const TextEncoding& charset,
    FetchParameters::DeferOption defer_option,
    Document& document,
    ResourceClient* link_client,
    RenderBlockingBehavior render_blocking_behavior) { ... 
resource_request.SetFetchPriorityHint(fetch_priority_hint);
 ResourceLoaderOptions options(context->GetCurrentWorld()); 
 >>> 
options.initiator_info.name = local_name;
 ... } ...  } ...  
```
### patch
```
  #if BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)
  initiator_info.dom_node_id =
      CoreProbeSink::HasAgentsGlobal(CoreProbeSink::kPageGraph)
          ? DOMNodeIds::IdForNode(client_->GetOwner())
          : kInvalidDOMNodeId;
  options.initiator_info
#endif  // BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)

```

