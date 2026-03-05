### match
```
...
// IWYU pragma: no_include <list>
 enum SkColorType : int 
 ; 
 >>> 
namespace gpu {
struct Mailbox;
}
 ... 
```
### patch
```
namespace {
bool AllowFingerprintingFromScriptState(blink::ScriptState* script_state) {
  return brave::AllowFingerprinting(
      blink::ExecutionContext::From(script_state),
      ContentSettingsType::BRAVE_WEBCOMPAT_CANVAS);
}

}  // namespace

```

### match
```
...
 namespace blink { ... 
 bool Canvas2DRecorderContext::IsAccelerated() const { ... 
return false;
 } 
 >>> 
 ... } ...  
```
### patch
```
bool Canvas2DRecorderContext::isPointInPath(ScriptState* script_state,
                                            const double x,
                                            const double y,
                                            const V8CanvasFillRule& winding) {
  if (!AllowFingerprintingFromScriptState(script_state)) {
    return false;
  }
  return isPointInPath(x, y, winding);
}

bool Canvas2DRecorderContext::isPointInPath(ScriptState* script_state,
                                            Path2D* dom_path,
                                            const double x,
                                            const double y,
                                            const V8CanvasFillRule& winding) {
  if (!AllowFingerprintingFromScriptState(script_state)) {
    return false;
  }
  return isPointInPath(dom_path, x, y, winding);
}

bool Canvas2DRecorderContext::isPointInStroke(ScriptState* script_state,
                                              const double x,
                                              const double y) {
  if (!AllowFingerprintingFromScriptState(script_state)) {
    return false;
  }
  return isPointInStroke(x, y);
}

bool Canvas2DRecorderContext::isPointInStroke(ScriptState* script_state,
                                              Path2D* dom_path,
                                              const double x,
                                              const double y) {
  if (!AllowFingerprintingFromScriptState(script_state)) {
    return false;
  }
  return isPointInStroke(dom_path, x, y);
}

```

