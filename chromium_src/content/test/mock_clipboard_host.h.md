### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
void WriteImage(const SkBitmap& bitmap) override;
 void CommitWrite() override; 
 >>> 
void ReadAvailableCustomAndStandardFormats(
      ReadAvailableCustomAndStandardFormatsCallback callback) override;
 ... } ...  
```
### patch
```cpp
  void SanitizeOnNextWriteText() override;

```

