### match
```cpp
...
 profile_(profile->GetOriginalProfile()) 
 , 
 >>>
```
### patch
```cpp
profile_to_check_(profile),

```

### match
```cpp
...
 
 std::unique_ptr<global_media_controls::MediaItemUIUpdatedView>
MediaDialogView::BuildMediaItemUIUpdatedView(
    const std::string& id,
    base::WeakPtr<media_message_center::MediaNotificationItem> item) { ... 
>>> 
 media_color_theme_ 
 , 
 show_devices 
 ) 
 , 
<<< 
...} ...  
```
### patch
```cpp
                          media_color_theme_, show_devices, profile_to_check_),

```

