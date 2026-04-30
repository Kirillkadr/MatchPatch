### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 class CONTENT_EXPORT ContentClient { ... 
// Gives the embedder a chance to register its own plugins.
 virtual void AddPlugins(std::vector<content::WebPluginInfo>* plugins) {} 
 >>> 
// Gives the embedder a chance to register the Content Decryption Modules
 ... } ...  } ...  
```
### patch
```cpp
  virtual void AddPlugins_ChromiumImpl(std::vector<content::WebPluginInfo>* plugins) {}

```

