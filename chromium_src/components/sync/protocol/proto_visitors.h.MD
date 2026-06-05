### match
```cpp
...
 
 namespace syncer { ... 
 
 VISIT_PROTO_FIELDS(const sync_pb::DeviceInfoSpecifics& proto) { ... 
VISIT(last_updated_timestamp);
 VISIT(feature_fields); 
 >>> 
VISIT(sharing_fields);
 ... } ...  } ...  
```
### patch
```cpp
  VISIT(brave_fields);

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 VISIT_PROTO_FIELDS(const sync_pb::FeatureSpecificFields& proto) { ... 
VISIT_ENUM(glic_experimental_triggering_state);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
VISIT_PROTO_FIELDS(const sync_pb::BraveSpecificFields& proto) {
  VISIT(is_self_delete_supported);                                     
}

```

