### match
```cpp
...
 
else {
    persistent_cache_files_[handle] = std::move(pending_backend);
  }
}
 >>> 
 ...
```
### patch
```cpp
#if BUILDFLAG(IS_WIN)
gpu::GPUInfo GpuHostImpl::Delegate::NotUsed() {
  return {};
}
void GpuHostImpl::DidGetExecutablePath(const std::string& path) {
  delegate_->DidGetExecutablePath(path);
}
#endif

```

