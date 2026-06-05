### match
```cpp
...
 
 namespace syncer { ... 
void set_last_get_key_failed(bool failed);
 void set_last_download_updates_result(const SyncerError result); 
 >>> 
void set_commit_result(const SyncerError result);
 ... } ...  
```
### patch
```cpp
  void set_last_server_error_message(const std::string& message); 

 public:
  const std::string& get_last_server_error_message() const;

```

