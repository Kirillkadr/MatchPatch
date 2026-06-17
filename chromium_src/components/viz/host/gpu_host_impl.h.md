### match
```cpp
...
 
 namespace viz { ... 
 
 Delegate { ... 
 virtual gpu::GPUInfo 
 GetGPUInfo() 
 const = 0 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
    #if BUILDFLAG(IS_WIN)
        virtual void DidGetExecutablePath(const std::string& path) {}
        virtual gpu::GPUInfo GetGPUInfo() const = 0;
    #endif

```

### match
```cpp
...
 
 namespace viz { ... 
 std::string GetShaderPrefixKey(); 
 >>> 
 ... } ...  
```
### patch
```cpp
  #if BUILDFLAG(IS_WIN)
  std::string NotUsed() {
    return {};
  }
  void DidGetExecutablePath(const std::string& path) override;
  std::string GetShaderPrefixKey();
    #endif

```

