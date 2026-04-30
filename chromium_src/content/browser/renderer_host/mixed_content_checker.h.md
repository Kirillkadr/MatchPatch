### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 class CONTENT_EXPORT MixedContentChecker { ... 
//
 // This mirrors `blink::MixedContentChecker::InWhichFrameIsContentMixed()`. 
 >>> 
RenderFrameHostImpl* InWhichFrameIsContentMixed(FrameTreeNode* node,
                                                  const GURL& url);
 ... } ...  } ...  
```
### patch
```cpp

  static bool DoesOriginSchemeRestrictMixedContent(const url::Origin& origin);
                                                                               

```

