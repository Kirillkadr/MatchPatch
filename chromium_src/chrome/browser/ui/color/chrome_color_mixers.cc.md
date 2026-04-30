### match
```cpp
...
 
 namespace { ... 
// .inc file serves to undefine the macros the first inclusion defined.
 #include "ui/color/color_id_map_macros.inc"
 
 >>> 
 ... } ...  
```
### patch
```cpp
// There are some new color mixers that we don't need to call here.
// Replace them with this empty color.
// As call order of color mixer is important, we call some of them
// from where we want to. Just changing order could overwrite previous
// colors.
void EmptyColorMixer(ui::ColorProvider* provider,
                     const ui::ColorProviderKey& key) {}

```

### match
```cpp
...
 
 void AddChromeColorMixers(ui::ColorProvider* provider,
                          const ui::ColorProviderKey& key) { ... 
AddTabStripColorMixer(provider, key);  >>> 
 AddMaterialChromeColorMixer(provider, key);  <<< 
AddMaterialNewTabPageColorMixer(provider, key);
 ... } ...  
```
### patch
```cpp
  EmptyColorMixer(provider, key);

```

### match
```cpp
...
 
 void AddChromeColorMixers(ui::ColorProvider* provider,
                          const ui::ColorProviderKey& key) { ... 
AddMaterialNewTabPageColorMixer(provider, key);  >>> 
 AddMaterialOmniboxColorMixer(provider, key); 
 AddMaterialSidePanelColorMixer(provider, key); 
 AddMaterialTabStripColorMixer(provider, key);  <<< 
// Must be the last one in order to override other mixer colors.
 ... } ...  
```
### patch
```cpp
  EmptyColorMixer(provider, key);
  EmptyColorMixer(provider, key);
  EmptyColorMixer(provider, key);

```

