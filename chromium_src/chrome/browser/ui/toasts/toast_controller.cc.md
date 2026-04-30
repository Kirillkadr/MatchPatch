### match
```cpp
...
>>>
 bool 
 ToastController::MaybeShowToast(ToastParams params) 
 {  <<< 
if (!CanShowToast(params.toast_id)) {
    RecordToastFailedToShow(params.toast_id);
    return false;
  }
 ... } ...  
```
### patch
```cpp
bool ToastController::MaybeShowToast_ChromiumImpl(ToastParams params) {

```

### match
```cpp
...
 
 bool ToastController::MaybeShowToast_ChromiumImpl(ToastParams params) { ... 
 
 if (!CanShowToast(params.toast_id)) { ... 
return false;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool ToastController::MaybeShowToast(ToastParams params) {
  if (params.toast_id == ToastId::kLinkCopied ||
      params.toast_id == ToastId::kImageCopied ||
      params.toast_id == ToastId::kAddedToReadingList) {
    return false;
  }
  return MaybeShowToast_ChromiumImpl(std::move(params));
}

```

