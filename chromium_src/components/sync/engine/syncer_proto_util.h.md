### match
```cpp
...
 
 namespace syncer { ... 
 
 class SyncerProtoUtil { ... 
static std::string SyncEntityDebugString(const sync_pb::SyncEntity& entry);
 // Set the protocol version field in the outgoing message. 
 >>> 
static void SetProtocolVersion(sync_pb::ClientToServerMessage* msg);
 ... } ...  } ...  
```
### patch
```cpp
  static void SaveServerErrorMessage(const sync_pb::ClientToServerResponse& response, 
                         StatusController* status_controller);
  friend class BraveSyncServerCommands;

```

