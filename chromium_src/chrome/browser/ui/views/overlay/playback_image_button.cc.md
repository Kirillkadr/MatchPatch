### match
```cpp
...
 
 PlaybackImageButton::PlaybackImageButton(PressedCallback callback)
    : OverlayWindowImageButton(std::move(callback)) { ... 
 
 ui::ImageModel::FromVectorIcon ( ... 
>>> 
 features::IsRoundedIconsEnabled() ? vector_icons::kPlayArrowFilledIcon
                                        : vector_icons::kPlayArrowOldIcon 
 , 
<<< 
...) ...  } ...
```
### patch
```cpp
features::IsRoundedIconsEnabled() ? ::kPlayArrowFilledIcon
                                        : ::kPlayArrowOldIcon,

```

### match
```cpp
...
 
 PlaybackImageButton::PlaybackImageButton(PressedCallback callback)
    : OverlayWindowImageButton(std::move(callback)) { ... 
 
 ui::ImageModel::FromVectorIcon ( ... 
>>> 
 features::IsRoundedIconsEnabled() ? vector_icons::kPauseFilledIcon
                                        : vector_icons::kPauseOldIcon 
 , 
<<< 
...) ...  } ...
```
### patch
```cpp
features::IsRoundedIconsEnabled() ? ::kPauseFilledIcon
                                        ::kPauseOldIcon,

```

### match
```cpp
...
>>> 
 features::IsRoundedIconsEnabled() ? vector_icons::kReplayIcon
                                        : vector_icons::kReplayOldIcon 
 , 
<<< 
...
```
### patch
```cpp
features::IsRoundedIconsEnabled() ? ::kLeoReloadIcon
                                        : ::kReplayOldIcon,

```

