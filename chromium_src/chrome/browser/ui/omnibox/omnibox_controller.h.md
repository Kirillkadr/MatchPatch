### match
```cpp
...
 
 class OmniboxController : public AutocompleteController::Observer { ... 
void SetView(OmniboxView* view);
 // The |current_url| field of input is only set for mobile ports. 
 >>> 
void StartAutocomplete(const AutocompleteInput& input) const;
 ... } ...  
```
### patch
```cpp
  void StartAutocomplete_ChromiumImpl(const AutocompleteInput& input) const;

```

### match
```cpp
...
 
 class OmniboxController : public AutocompleteController::Observer { ... 
// optionally start a prefetch request to warm up the their underlying
 // service(s) and/or optionally cache their otherwise async response. 
 >>> 
void StartZeroSuggestPrefetch();
 ... } ...  
```
### patch
```cpp

  // Per security/privacy team, we want to disable zero suggest prefetch.
  void StartZeroSuggestPrefetch_Unused();

```

