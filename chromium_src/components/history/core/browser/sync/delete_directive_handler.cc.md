### match
```cpp
...
 
 namespace history { ...   >>> 
 bool 
 DeleteDirectiveHandler::CreateUrlDeleteDirective(const GURL& url) 
 {  <<< 
DCHECK(url.is_valid());
 ... } ...  } ...  
```
### patch
```cpp
bool DeleteDirectiveHandler::CreateUrlDeleteDirective_ChromiumImpl(const GURL& url) {

```

### match
```cpp
...
 
 namespace history { ... 
 
 void DeleteDirectiveHandler::FinishProcessing(
    PostProcessingAction post_processing_action,
    const syncer::SyncDataList& delete_directives) { ... 
if (sync_processor_.get() &&
      post_processing_action == DROP_AFTER_PROCESSING) {
    syncer::SyncChangeList change_list;
    for (const syncer::SyncData& delete_directive : delete_directives) {
      change_list.push_back(syncer::SyncChange(
          FROM_HERE, syncer::SyncChange::ACTION_DELETE, delete_directive));
    }
    sync_processor_->ProcessSyncChanges(FROM_HERE, change_list);
  }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool DeleteDirectiveHandler::CreateUrlDeleteDirective(const GURL& url) {
  return false;
}

```

