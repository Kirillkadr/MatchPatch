### match
```cpp
...
>>>
#if BUILDFLAG(IS_ANDROID)
  void InitializeWithHost(
      mojo::PendingRemote<mojom::GpuHost> gpu_host,
      gpu::GpuProcessShmCount use_shader_cache_shm_count,
      scoped_refptr<gl::GLSurface> default_offscreen_surface,
      mojom::GpuServiceCreationParamsPtr creation_params,
      gpu::SyncPointManager* sync_point_manager = nullptr,
      gpu::SharedImageManager* shared_image_manager = nullptr,
      gpu::Scheduler* scheduler = nullptr,
      base::WaitableEvent* shutdown_event = nullptr,
      const gpu::SharedContextState::GrContextOptionsProvider*
          gr_context_options_provider = nullptr);
#else
  void InitializeWithHost(
      mojo::PendingRemote<mojom::GpuHost> gpu_host,
      gpu::GpuProcessShmCount use_shader_cache_shm_count,
      scoped_refptr<gl::GLSurface> default_offscreen_surface,
      mojom::GpuServiceCreationParamsPtr creation_params,
      base::WaitableEvent* shutdown_event = nullptr);
#endif
<<<
...
```
### patch
```cpp
#if BUILDFLAG(IS_ANDROID)
  void InitializeWithHost_ChromiumImpl(
      mojo::PendingRemote<mojom::GpuHost> gpu_host,
      gpu::GpuProcessShmCount use_shader_cache_shm_count,
      scoped_refptr<gl::GLSurface> default_offscreen_surface,
      mojom::GpuServiceCreationParamsPtr creation_params,
      gpu::SyncPointManager* sync_point_manager = nullptr,
      gpu::SharedImageManager* shared_image_manager = nullptr,
      gpu::Scheduler* scheduler = nullptr,
      base::WaitableEvent* shutdown_event = nullptr,
      const gpu::SharedContextState::GrContextOptionsProvider*
          gr_context_options_provider = nullptr);
  void InitializeWithHost(
      mojo::PendingRemote<mojom::GpuHost> gpu_host,
      gpu::GpuProcessShmCount use_shader_cache_shm_count,
      scoped_refptr<gl::GLSurface> default_offscreen_surface,
      mojom::GpuServiceCreationParamsPtr creation_params,
      gpu::SyncPointManager* sync_point_manager = nullptr,
      gpu::SharedImageManager* shared_image_manager = nullptr,
      gpu::Scheduler* scheduler = nullptr,
      base::WaitableEvent* shutdown_event = nullptr,
      const gpu::SharedContextState::GrContextOptionsProvider*
          gr_context_options_provider = nullptr);
#else
  void InitializeWithHost_ChromiumImpl(
      mojo::PendingRemote<mojom::GpuHost> gpu_host,
      gpu::GpuProcessShmCount use_shader_cache_shm_count,
      scoped_refptr<gl::GLSurface> default_offscreen_surface,
      mojom::GpuServiceCreationParamsPtr creation_params,
      base::WaitableEvent* shutdown_event = nullptr);

  void InitializeWithHost(
      mojo::PendingRemote<mojom::GpuHost> gpu_host,
      gpu::GpuProcessShmCount use_shader_cache_shm_count,
      scoped_refptr<gl::GLSurface> default_offscreen_surface,
      mojom::GpuServiceCreationParamsPtr creation_params,
      base::WaitableEvent* shutdown_event = nullptr);
#endif

```

