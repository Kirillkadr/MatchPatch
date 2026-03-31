### match
```cpp
...
 
 # ifndef ... 
 
 class HistoryQuickProvider : public HistoryProvider { ... 
~HistoryQuickProvider() override;
 // Performs the autocomplete matching and scoring. 
 >>> 
void DoAutocomplete();
 ... } ...  
```
### patch
```cpp
  void DoAutocompleteUnused();                 
  friend class BraveHistoryQuickProvider;

```

