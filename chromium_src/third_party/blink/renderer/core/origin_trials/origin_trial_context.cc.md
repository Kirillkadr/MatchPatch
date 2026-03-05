### match
```
...
 namespace blink { ...   >>> 
 void 
 OriginTrialContext::AddFeature(mojom::blink::OriginTrialFeature feature) 
 {  <<< ... 
enabled_features_.insert(feature);
 ... } ...  } ...  
```
### patch
```
void OriginTrialContext::AddFeature_ChromiumImpl(mojom::blink::OriginTrialFeature feature) {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 OriginTrialContext::AddForceEnabledTrials 
 (  <<< ... 
const Vector<String>& trial_names
 ... ) ...  } ...  
```
### patch
```
void OriginTrialContext::AddForceEnabledTrials_ChromiumImpl(

```

### match
```
...
 namespace blink { ... 
 void OriginTrialContext::SendTokenToBrowser(
    const OriginInfo& origin_info,
    const TrialToken& parsed_token,
    const String& raw_token,
    const Vector<OriginInfo>* script_origin_info) { ... 
context_->GetRuntimeFeatureStateOverrideContext()->EnablePersistentTrial(
      raw_token, std::move(script_origins));
 } 
 >>> 
 ... } ...  
```
### patch
```
// AddFeature doesn't check if origin_trials::IsTrialValid.
void OriginTrialContext::AddFeature(blink::mojom::OriginTrialFeature feature) {
  if (origin_trials::IsTrialDisabledInBrave(feature))
    return;
  AddFeature_ChromiumImpl(feature);
}

// AddForceEnabledTrials only has a DCHECK with origin_trials::IsTrialValid.
void OriginTrialContext::AddForceEnabledTrials(
    const Vector<String>& trial_names) {
  for (const String& trial_name : trial_names) {
    if (origin_trials::IsTrialDisabledInBrave(trial_name.Utf8()))
      return;
  }

  AddForceEnabledTrials_ChromiumImpl(trial_names);
}

```

