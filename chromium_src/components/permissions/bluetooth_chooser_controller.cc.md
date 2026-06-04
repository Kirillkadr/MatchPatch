### match
```cpp
...
 
 namespace permissions { ... 
int BluetoothChooserController::GetAuthorizeBluetoothLinkTextMessageId() const {
  return IDS_BLUETOOTH_DEVICE_CHOOSER_AUTHORIZE_BLUETOOTH_LINK_TEXT;
}
 } 
 // namespace permissions 
 >>> 
 ... 
```
### patch
```cpp
namespace permissions {

std::optional<ChooserControllerType> BluetoothChooserController::GetType()
    const {
  return ChooserControllerType::kBluetooth;
}

}  // namespace permissions
```

