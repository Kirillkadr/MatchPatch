### match
```cpp
...
 
 # ifndef ... 
 
 class ContentSettingImageModel { ... 
virtual ~ContentSettingImageModel() = default;
 // Generates a vector of all image models to be used within one window. 
 >>> 
static std::vector<std::unique_ptr<ContentSettingImageModel>>
  GenerateContentSettingImageModels();
 ... } ...  
```
### patch
```cpp
  static std::vector<std::unique_ptr<ContentSettingImageModel>>
  GenerateContentSettingImageModels_ChromiumImpl();

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ContentSettingImageModel { ... 
// A special case for framebusting since that does not have a
 // ContentSettingsType. 
 >>> 
void SetFramebustBlockedIcon();
 ... } ...  
```
### patch
```cpp
  void  GetIconFromType(ContentSettingsType type, bool blocked,
                          raw_ptr<const gfx::VectorIcon>* icon,
                        raw_ptr<const gfx::VectorIcon>* badge);

```

