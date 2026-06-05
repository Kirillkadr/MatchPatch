### match
```cpp
...
 
 namespace syncer { ... 
 
 class MetadataBatch { ... 
const sync_pb::DataTypeState& GetDataTypeState() const;
 // Set the DataTypeState for this batch. 
 >>> 
void SetDataTypeState(const sync_pb::DataTypeState& state);
 ... } ...  } ...  
```
### patch
```cpp
  void ClearProgressToken();  

```

