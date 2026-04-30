### match
```cpp
...
 
 void AddMaterialOmniboxColorMixer(ui::ColorProvider* provider,
                                  const ui::ColorProviderKey& key) { ...   >>> 
 if (!ShouldApplyChromeMaterialOverrides(key)) {
    return;
  } 
 // While both design systems continue to exist, the material recipes are 
 // intended to leverage the existing chrome color mixers, overriding when 
 // required to do so according to the new material spec. 
 // TODO(crbug.com/40883435): Update color recipes to match UX mocks. 
 ui::ColorMixer& mixer = provider->AddMixer(); 
 mixer[kColorLocationBarClearAllButtonIcon] = {ui::kColorSysOnSurfaceSubtle}; 
 mixer[kColorLocationBarClearAllButtonIconDisabled] =
      ui::GetResultingPaintColor(ui::kColorSysStateDisabled,
                                 kColorLocationBarClearAllButtonIcon); 
 mixer[kColorToolbarBackgroundSubtleEmphasis] = {
      ui::kColorSysOmniboxContainer}; 
 mixer[kColorToolbarBackgroundSubtleEmphasisHovered] =
      ui::GetResultingPaintColor(ui::kColorSysStateHoverBrightBlendProtection,
                                 kColorToolbarBackgroundSubtleEmphasis);  <<<  ...} ...  
```
### patch
```cpp
  // Upstream's material omnibox colors are currently not used.

```

