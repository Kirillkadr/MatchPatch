### match
```cpp
...
 
 namespace download { ... 
 
 std::string BackgroundDownloadClientToString(DownloadClient client) { ... 
 
 case DownloadClient : ... 
 return "Bruschetta"; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
    case DownloadClient::CUSTOM_LIST_SUBSCRIPTIONS:  
      return "CustomListSubscriptions";

```

