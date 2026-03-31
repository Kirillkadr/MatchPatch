### match
```cpp
...
 
 # ifndef ... 
 
 class ShortcutsBackend : public RefcountedKeyedService,
                         public history::HistoryServiceObserver,
                         public TemplateURLServiceObserver { ... 
// Internal initialization of the back-end. Posted by Init() to the DB thread.
 // On completion posts InitCompleted() back to UI thread. 
 >>> 
void InitInternal();
 ... } ...  
```
### patch
```cpp
  friend class BraveShortcutsProviderTest;

```

