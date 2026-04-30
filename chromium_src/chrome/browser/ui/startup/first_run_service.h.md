### match
```cpp
...
std::unique_ptr<ProfileNameResolver> profile_name_resolver_;
 ResumeTaskCallback resume_task_callback_; 
 >>> 
base::WeakPtrFactory<FirstRunService> weak_ptr_factory_{this};
 ... 
```
### patch
```cpp
  friend class FirstRunServiceTest_FinishProfileSetUpShouldNotChangeName_Test;

```

