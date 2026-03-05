### match
```
...
 namespace blink { ... 
 int MediaValuesDynamic::DeviceWidth() const { ...   >>> 
 return CalculateDeviceWidth(frame_);  <<< ... } ...  } ...  
```
### patch
```
  return CalculateDeviceWidth(frame_, /* early = */ false);

```

### match
```
...
 namespace blink { ... 
 int MediaValuesDynamic::DeviceHeight() const { ...   >>> 
 return CalculateDeviceHeight(frame_);  <<< ... } ...  } ...  
```
### patch
```
  return CalculateDeviceHeight(frame_, /* early = */ false);

```

