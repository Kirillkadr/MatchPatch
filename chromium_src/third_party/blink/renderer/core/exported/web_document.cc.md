### match
```
...
 namespace blink { ... 
 void WebDocument::DispatchAutofillEvent(
    std::vector<std::pair<WebFormControlElement, WebString>> field_data,
    const base::UnguessableToken& fill_id,
    bool supports_refill) { ... 
document->DispatchAutofillEvent(std::move(converted_field_data), fill_id,
                                  supports_refill);
 } 
 >>> 
 ... } ...  
```
### patch
```
bool WebDocument::IsDOMFeaturePolicyEnabled(v8::Isolate* isolate,
                                            v8::Local<v8::Context> context,
                                            const WebString& feature) {
  blink::ScriptState* script_state = blink::ScriptState::From(isolate, context);
  Document* document = Unwrap<Document>();
  return document->featurePolicy()->allowsFeature(script_state, feature);
}

```

