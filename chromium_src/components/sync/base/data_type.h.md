### match
```cpp
...
 
 namespace syncer { ... 
// low-priority types has been downloaded (which may be a lot of data).
>>> 
 DataTypeSet LowPriorityUserTypes(); 
<<< 
// Returns a list of all control types.
 ... } ...  
```
### patch
```cpp
DataTypeSet LowPriorityUserTypes_ChromiumImpl();

```

### match
```cpp
...
 
 namespace syncer { ... 
// clients.
 bool IsActOnceDataType(DataType data_type); 
 >>> 
 ... } ...  
```
### patch
```cpp
constexpr DataTypeSet LowPriorityUserTypes() {
  auto low_priority_user_types = LowPriorityUserTypes_ChromiumImpl();
  // Directives must be synced after history entities. If
  // history delete directives are processed before retrieving history upon
  // initial sync, relevant entries will not be deleted.
  // This override must be reverted when
  // https://github.com/brave/go-sync/issues/178 will be solved.
  low_priority_user_types.Remove(HISTORY);
  low_priority_user_types.Put(HISTORY_DELETE_DIRECTIVES);
  return low_priority_user_types;
}

```

