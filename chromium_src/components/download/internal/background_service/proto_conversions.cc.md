### match
```cpp
...
 
 namespace download { ... 
 
 protodb::DownloadClient ProtoConversions::DownloadClientToProto(
    DownloadClient client) { ... 
 
 case DownloadClient : ... 
 return protodb::DownloadClient::BOUNDARY; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
    case DownloadClient::CUSTOM_LIST_SUBSCRIPTIONS:
    return protodb::DownloadClient::CUSTOM_LIST_SUBSCRIPTIONS;

```

### match
```cpp
...
 
 namespace download { ... 
 
 DownloadClient ProtoConversions::DownloadClientFromProto(
    protodb::DownloadClient client) { ... 
 
 case protodb : ... 
 return DownloadClient::BOUNDARY; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
    case protodb::DownloadClient::CUSTOM_LIST_SUBSCRIPTIONS: 
    return DownloadClient::CUSTOM_LIST_SUBSCRIPTIONS;

```

