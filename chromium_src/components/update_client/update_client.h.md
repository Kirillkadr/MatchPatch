### match
```cpp
...
 
 namespace update_client { ... 
 
 class CrxInstaller : public base::RefCountedThreadSafe<CrxInstaller> { ... 
// be uninstalled from disk. Returns true if uninstallation is supported,
 // and false otherwise. 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  virtual bool IsBraveComponent() const;

```

### match
```cpp
...
 
 namespace update_client { ... 
 // Creates an instance of the update client. 
 >>> 
 ... } ...  
```
### patch
```cpp
scoped_refptr<UpdateClient> UpdateClientFactory_ChromiumImpl(scoped_refptr<Configurator> config); 

```

