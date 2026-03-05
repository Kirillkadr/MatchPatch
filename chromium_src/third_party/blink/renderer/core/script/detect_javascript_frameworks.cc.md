### match
```
...
 namespace blink { ...   >>> 
 void 
 DetectJavascriptFrameworksOnLoad(Document& document) 
 {  <<< ... 
LocalFrame* const frame = document.GetFrame();
 ... } ...  } ...  
```
### patch
```
void DetectJavascriptFrameworksOnLoad_Unused(Document& document) {

```

### match
```
...
 namespace blink { ... 
 void DetectJavascriptFrameworksOnLoad_Unused(Document& document) { ... 
TraverseTreeForFrameworks(document, isolate, context);
 } 
 >>> 
 ... } ...  
```
### patch
```
// NOLINTNEXTLINE(runtime/references)
void DetectJavascriptFrameworksOnLoad(Document& document) {}

```

