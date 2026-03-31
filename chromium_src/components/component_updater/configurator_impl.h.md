### match
```cpp
...
 
 # ifndef ... 
 
 namespace component_updater { ... 
 
 class ConfiguratorImpl { ... 
// True means that the background downloader can be used for downloading
 // non on-demand components. 
 >>> 
bool EnabledBackgroundDownloader() const;
 ... } ...  } ...  
```
### patch
```cpp
  bool EnabledBackgroundDownloader_Unused() const;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace component_updater { ... 
 
 class ConfiguratorImpl { ... 
bool EnabledBackgroundDownloader() const;
 // True if signing of update checks is enabled. 
 >>> 
bool EnabledCupSigning() const;
 ... } ...  } ...  
```
### patch
```cpp
  bool EnabledCupSigning_Unused() const; 

```

