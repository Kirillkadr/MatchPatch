### match
```cpp
...
 
 # ifndef ... 
 
 namespace browser_sync { ... 
// syncable.  >>> 
 std::optional<sync_preferences::SyncablePrefMetadata> GetSyncablePrefMetadata(
      std::string_view pref_name) const override;  <<< 
std::map<std::string_view, sync_preferences::SyncablePrefMetadata>
  GetAllSyncablePrefsForTest() const;
 ... } ...  
```
### patch
```cpp
  std::optional<sync_preferences::SyncablePrefMetadata> GetSyncablePrefMetadata_ChromiumImpl(std::string_view pref_name) const;
  std::optional<sync_preferences::SyncablePrefMetadata>    
  GetSyncablePrefMetadata(std::string_view pref_name) const override;

```

