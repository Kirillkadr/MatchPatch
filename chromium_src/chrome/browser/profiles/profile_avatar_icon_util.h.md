### match
```cpp
...
 
 # ifndef ... 
 
 namespace profiles { ... 
 size_t avatar_size 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
#if !BUILDFLAG(IS_CHROMEOS) && !BUILDFLAG(IS_ANDROID)
inline constexpr size_t kBraveDefaultAvatarIconsCount = 34;
#else
inline constexpr size_t kBraveDefaultAvatarIconsCount = 0;
#endif

// Provide direct access to custom implementation
base::DictValue GetDefaultProfileAvatarIconAndLabel_Brave(SkColor fill_color,
                                                          SkColor stroke_color,
                                                          bool selected);

```

