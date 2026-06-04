### match
```cpp
...
 
 namespace permissions { ... 
 
 base::WeakPtr<BluetoothScanningPromptController>
BluetoothScanningPromptController::GetWeakPtr() { ... 
return weak_factory_.GetWeakPtr();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
std::optional<ChooserControllerType>
BluetoothScanningPromptController::GetType() const {
  return ChooserControllerType::kBluetooth;
}

```

