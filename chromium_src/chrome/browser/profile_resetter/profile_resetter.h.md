### match
```cpp
...
 
 # ifndef ... 
void MarkAsDone(Resettable resettable);  >>> 
 void ResetDefaultSearchEngine();  <<< 
void ResetHomepage();
 ... 
```
### patch
```cpp
  friend class BraveProfileResetter;
  virtual void ResetDefaultSearchEngine();

```

