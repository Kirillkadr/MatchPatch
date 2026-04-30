### match
```cpp
...
 
 namespace content { ... 
WebContents::ScopedIgnoreInputEvents::ScopedIgnoreInputEvents(
    base::OnceClosure on_destruction_cb)
    : on_destruction_cb_(std::move(on_destruction_cb)) {}
 } 
 // namespace content 
 >>> 
 ... 
```
### patch
```cpp

namespace content {

bool WebContents::GetShouldDoLearningForTesting() {
  return true;
}

}  // namespace content

```

