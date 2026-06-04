### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
COMPONENT_EXPORT(PERMISSIONS_COMMON)  >>> 
 extern const char kChooserBluetoothOverviewURL[];  <<< 
// The URL for the Embedded Content help center article in the SAA permission
 ... } ...  
```
### patch
```cpp
extern const char kChooserBluetoothOverviewURL_ChromeOverride[];
COMPONENT_EXPORT(PERMISSIONS_COMMON)
extern const char kChooserBluetoothOverviewURL[];

```

