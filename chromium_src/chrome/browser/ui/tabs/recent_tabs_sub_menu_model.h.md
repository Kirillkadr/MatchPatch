### match
```cpp
...
size_t last_local_model_index_ = 0;
 base::CancelableTaskTracker local_tab_cancelable_task_tracker_; 
 >>> 
base::ScopedObservation<sessions::TabRestoreService,
                          sessions::TabRestoreServiceObserver>
      tab_restore_service_observation_{this};
 ... 
```
### patch
```cpp
  std::unique_ptr<sessions::SessionTab> stub_tab_; 
  friend class BraveRecentTabsSubMenuModel;

```

