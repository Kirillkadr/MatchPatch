### match
```cpp
...
// shown, otherwise return false.
 virtual bool MaybeShowToast(ToastParams params); 
 >>> 
using WidgetDestroyedCallback = base::RepeatingCallback<void(ToastId)>;
 ... 
```
### patch
```cpp
  bool MaybeShowToast_ChromiumImpl(ToastParams params);

```

