### match
```cpp
...
 
 # ifndef ... 
 
 class OnDeviceHeadProvider : public AutocompleteProvider { ... 
 friend class OnDeviceHeadProviderTest; 
 >>> 
// A useful data structure to store Autocomplete input and suggestions fetched
 ... } ...  
```
### patch
```cpp
  friend class BraveOnDeviceHeadProvider;

```

