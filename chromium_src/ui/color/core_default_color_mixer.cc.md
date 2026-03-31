### match
```cpp

...
>>>
 void 
 AddCoreDefaultColorMixer 
 ( 
 ColorProvider* provider 
 ,  <<< ... 
const ColorProviderKey& key
 ... ) ...  
```
### patch
```cpp

void AddCoreDefaultColorMixer_Chromium(ColorProvider* provider,

```

### match
```cpp

...
 namespace ui { ... 
 void AddCoreDefaultColorMixer_Chromium(ColorProvider* provider,
const ColorProviderKey& key) { ... 
mixer[kColorTextSelectionForeground] =
      GetColorWithMaxContrast(kColorTextSelectionBackground);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp

void AddBraveCoreDefaultColorMixer(ColorProvider* provider,
                                   const ColorProviderKey& key) {
  ColorMixer& mixer = provider->AddMixer();
  const bool dark_mode = key.color_mode == ColorProviderKey::ColorMode::kDark;

  mixer[kColorAlertMediumSeverityIcon] = {
      dark_mode ? SkColorSetRGB(0xBB, 0x88, 0x00)
                : SkColorSetRGB(0xE2, 0xA5, 0x00)};
}

void AddCoreDefaultColorMixer(ColorProvider* provider,
                              const ColorProviderKey& key) {
  AddCoreDefaultColorMixer_Chromium(provider, key);
  AddBraveCoreDefaultColorMixer(provider, key);
}

```

