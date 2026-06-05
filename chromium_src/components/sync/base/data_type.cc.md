### match
```cpp
...
 
 namespace syncer { ... 
>>> 
 DataTypeSet 
 EncryptableUserTypes() 
 { 
<<< 
DataTypeSet encryptable_user_types;
 ... } ...  } ...  
```
### patch
```cpp
DataTypeSet EncryptableUserTypes_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 bool IsActOnceDataType(DataType data_type) { ... 
return data_type == HISTORY_DELETE_DIRECTIVES;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
DataTypeSet EncryptableUserTypes() {
  DataTypeSet encryptable_user_types = EncryptableUserTypes_ChromiumImpl();
  // Brave sync has encryption setup ready when sync chain created
  encryptable_user_types.Put(DEVICE_INFO);
  encryptable_user_types.Put(HISTORY);
  return encryptable_user_types;
}

```

