### match
```cpp
...
 
 namespace syncer { ... 
 
 void MetadataBatch::SetDataTypeState(const sync_pb::DataTypeState& state) { ... 
state_ = state;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void MetadataBatch::ClearProgressToken() {
  state_.mutable_progress_marker()->clear_token();
}

```

