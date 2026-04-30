### match
```cpp
...
 
 namespace { ... 
 
 NSString* AppGroupPrefix() { ...   >>> 
 NSBundle* bundle = base::apple::FrameworkBundle();  <<< 
NSDictionary* infoDictionary = bundle.infoDictionary;
 ... } ...  } ...  
```
### patch
```cpp
  NSBundle* bundle = base::apple::MainBundle();

```

### match
```cpp
...
 
 NSURL* CredentialProviderSharedArchivableStoreURL() { ... 
 
 if (!groupURL) { ...   >>> 
 NSBundle* bundle = base::apple::FrameworkBundle();  <<< 
NSNumber* isEarlGreyTest =
        [bundle objectForInfoDictionaryKey:@"CRIsEarlGreyTest"];
 ... } ...  } ...  
```
### patch
```cpp
    NSBundle* bundle = base::apple::MainBundle();

```

