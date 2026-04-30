### match
```cpp
...
>>>
 void 
 AddMaterialTabStripColorMixer 
 ( 
 ui::ColorProvider* provider 
 ,  <<< 
const ui::ColorProviderKey& key
 ... ) ...  
```
### patch
```cpp
void AddMaterialTabStripColorMixer_ChromiumImpl(ui::ColorProvider* provider,

```

### match
```cpp
...
 
 void AddMaterialTabStripColorMixer_ChromiumImpl(ui::ColorProvider* provider,
const ui::ColorProviderKey& key) { ... 
mixer[kColorTabSearchButtonCRForegroundFrameInactive] = {
      ui::kColorSysOnSurfacePrimaryInactive};
 } 
 >>> 
 ... 
```
### patch
```cpp

void AddMaterialTabStripColorMixer(ui::ColorProvider* provider,
                                   const ui::ColorProviderKey& key) {
  // Upstream's material tab strip colors are currently not used.
}
```

