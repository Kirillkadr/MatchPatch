### match
```cpp

...
 namespace ui { ... 
 void AddColorMixers(ColorProvider* provider, const ColorProviderKey& key) { ... 
 AddRefColorMixer(provider, key); 
 >>> 
// TODO(tluk): Determine the correct place to insert the sys color mixer.
 ... } ...  } ...  
```
### patch
```cpp

  AddRefColorMixer(provider, key);
  AddBraveRefColorMixer(provider, key);
  nala::AddNalaColorMixer(provider, key)

```

