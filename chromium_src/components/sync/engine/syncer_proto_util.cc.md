### match
```cpp
...
 
 namespace syncer { ... 
 
 SyncerError SyncerProtoUtil::HandleClientToServerMessageResponse(
    const sync_pb::ClientToServerResponse& response,
    SyncCycle* cycle,
    DataTypeSet* partial_failure_data_types) { ... 
 GetProtocolErrorFromResponse(response, cycle->context()) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
        SaveServerErrorMessage(response, cycle->mutable_status_controller());

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 std::string SyncerProtoUtil::ClientToServerResponseDebugString(
    const ClientToServerResponse& response) { ... 
return output;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// static
void SyncerProtoUtil::SaveServerErrorMessage(
    const sync_pb::ClientToServerResponse& response,
    StatusController* status_controller) {
  if (response.has_error_message()) {
    status_controller->set_last_server_error_message(response.error_message());
  } else {
    status_controller->set_last_server_error_message(std::string());
  }
}

```

