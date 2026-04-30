### match
```cpp
...
 
 class AutocompleteController : public AutocompleteProviderListener,
                               public base::trace_event::MemoryDumpProvider { ... 
friend class FakeSuggestionsAutocompleteController;
 #endif 
 >>> 
 ... } ...  
```
### patch
```cpp
  OmniboxPromotionTest;
  friend class AutocompleteControllerTest

```

### match
```cpp
...
 
 # ifndef ... 
 
 class AutocompleteController : public AutocompleteProviderListener,
                               public base::trace_event::MemoryDumpProvider { ... 
AutocompleteControllerConfig config_;
 } 
 ; 
 >>> 
 ... 
```
### patch
```cpp
namespace ai_chat {
void MaybeShowLeoMatch(AutocompleteResult* result);
}

```

