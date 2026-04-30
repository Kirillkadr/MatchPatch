### match
```cpp
...
 
 # ifndef ... 
 
 class BookmarkProvider : public AutocompleteProvider { ... 
// Performs the actual matching of |input| over the bookmarks and fills in
 // |matches_|. 
 >>> 
void DoAutocomplete(const AutocompleteInput& input);
 ... } ...  
```
### patch
```cpp
  friend class BraveBookmarkProvider;

```

