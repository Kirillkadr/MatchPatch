### match
```cpp
...
 
 uint32_t PrefService::GetWriteFlags(const PrefService::Preference* pref) { ... 
return write_flags;
 } 
 >>> 
 ... 
```
### patch
```cpp
bool PrefService::GetBooleanOr(const std::string& path, bool other) const {
  return GetBoolean(path) || other;
}
```

