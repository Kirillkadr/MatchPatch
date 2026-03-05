### match
```
...
 namespace blink { ... 
 MediaValuesCached::MediaValuesCachedData::MediaValuesCachedData(
    Document& document)
    : MediaValuesCached::MediaValuesCachedData() { ... 
 if (frame && frame->View()) { ... 
dynamic_viewport_height =
        MediaValues::CalculateDynamicViewportHeight(frame);  >>> 
 device_width = MediaValues::CalculateDeviceWidth(frame); 
 device_height = MediaValues::CalculateDeviceHeight(frame);  <<< ... 
device_pixel_ratio = MediaValues::CalculateDevicePixelRatio(frame);
 ... } ...  } ...  } ...  
```
### patch
```
    device_width = MediaValues::CalculateDeviceWidth(frame, /* early = */ true);
    device_height = MediaValues::CalculateDeviceHeight(frame, /* early = */ true);

```

