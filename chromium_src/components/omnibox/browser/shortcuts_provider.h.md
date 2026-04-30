### match
```cpp
...
 
 # ifndef ... 
 
 class ShortcutsProvider : public AutocompleteProvider,
                          public ShortcutsBackend::ShortcutsBackendObserver { ... 
// with scoring signals for ML models if enabled. Only populates signals for
 // ULR matches for now. 
 >>> 
void DoAutocomplete(const AutocompleteInput& input,
                      bool populate_scoring_signals);
 ... } ...  
```
### patch
```cpp
  friend class BraveShortcutsProvider; 

```

