### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT OriginTrialContext final
    : public GarbageCollected<OriginTrialContext> { ... 
// Forces a given origin-trial-enabled feature to be enabled in this context
 // and immediately adds required bindings to already initialized JS contexts. 
 >>> 
void AddFeature(mojom::blink::OriginTrialFeature feature);
 ... } ...  } ...  
```
### patch
```
  void AddFeature_ChromiumImpl(blink::mojom::OriginTrialFeature feature);

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT OriginTrialContext final
    : public GarbageCollected<OriginTrialContext> { ... 
// Forces given trials to be enabled in this context and immediately adds
 // required bindings to already initialized JS contexts. 
 >>> 
void AddForceEnabledTrials(const Vector<String>& trial_names);
 ... } ...  } ...  
```
### patch
```
  void AddForceEnabledTrials_ChromiumImpl(const Vector<String>& trial_names);

```

