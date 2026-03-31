### match
```cpp
...
 
 # ifndef ... 
// This does not update |done_|.  >>> 
 void DoHistoryQuery(bool minimal_changes);  <<< 
// Returns the time to delay before sending the Suggest request.
 ... 
```
### patch
```cpp
  void DoHistoryQueryUnused();                                     
  friend class BraveSearchProvider;
  friend class BraveSearchProviderTest;
  bool IsBraveRichSuggestion(bool is_keyword);

 public:
  virtual class BraveSearchProvider* AsBraveSearchProvider();

 private:
  virtual void DoHistoryQuery(bool minimal_changes);

```

