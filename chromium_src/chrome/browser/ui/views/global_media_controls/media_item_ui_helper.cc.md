### match
```cpp
...
>>>
 BuildDeviceSelector 
 ( 
<<< 
...) ...  
```
### patch
```cpp
BuildDeviceSelector_ChromiumImpl(

```

### match
```cpp
...
 
 const gfx::VectorIcon& GetVectorIcon(
    global_media_controls::mojom::IconType icon) { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp
std::unique_ptr<global_media_controls::MediaItemUIDeviceSelector>
BuildDeviceSelector(
    const std::string& id,
    base::WeakPtr<media_message_center::MediaNotificationItem> item,
    global_media_controls::mojom::DeviceService* device_service,
    MediaItemUIDeviceSelectorDelegate* selector_delegate,
    Profile* profile,
    global_media_controls::GlobalMediaControlsEntryPoint entry_point,
    bool show_devices,
    std::optional<media_message_center::MediaColorTheme> media_color_theme,
    Profile* profile_to_check) {
  if (profile_to_check && profile_to_check->IsTor()) {
    return nullptr;
  }
  return BuildDeviceSelector_ChromiumImpl(
      id, std::move(item), device_service, selector_delegate, profile,
      entry_point, show_devices, std::move(media_color_theme));
}
```

