### match
```cpp
...
 
 
void HistoryBackend::StartDeletingForeignVisits() {
  ProcessDBTask(std::make_unique<DeleteForeignVisitsDBTask>(), task_runner_,
                /*is_canceled=*/base::BindRepeating([]() { return false; }));
} 
 >>> 
 ...
```
### patch
```cpp
HistoryCountResult HistoryBackend::GetKnownToSyncCount() {
  int count = 0;
  return {db_ && db_->GetKnownToSyncCount(&count), count};
}

```

