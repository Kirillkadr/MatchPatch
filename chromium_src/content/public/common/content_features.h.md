### match
```cpp
...
 
 # ifndef ... 
 
 namespace features { ... 
#if BUILDFLAG(IS_ANDROID)
CONTENT_EXPORT bool IsFluidResizeEnabled();
#endif
 } 
 // namespace features 
 >>> 
 ... 
```
### patch
```cpp
namespace features {
CONTENT_EXPORT BASE_DECLARE_FEATURE(kIdleDetection);

}  // namespace features

```

