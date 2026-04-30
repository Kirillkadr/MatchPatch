### match
```cpp
...
 
 # ifndef ... 
 
 class LocalHistoryZeroSuggestProvider : public AutocompleteProvider { ... 
// Queries the keyword search terms table of the in-memory URLDatabase for the
 // recent search terms submitted to the default search provider. 
 >>> 
void QueryURLDatabase(const AutocompleteInput& input);
 ... } ...  
```
### patch
```cpp
  void QueryURLDatabase_Unused();                         
  friend class BraveLocalHistoryZeroSuggestProvider;

```

