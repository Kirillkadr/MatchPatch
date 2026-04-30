### match
```cpp
...
 
 namespace net { ... 
 
 HostCache::Entry HostCache::Entry::CopyWithDefaultPort(uint16_t port) const { ... 
if (hostname.port() == 0) {
      hostname.set_port(port);
    }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
  if (!text_records().empty()) {
    std::vector<std::string> copy_text_records;
    for (const auto& record : text_records())
      copy_text_records.push_back(record);
    copy.set_text_records(std::move(copy_text_records)); 
  }

```

