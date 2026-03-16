### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
// platforms this `skip_session_components` is expected to be unset.  >>> 
 void AddDefaultComponentExtensions(bool skip_session_components);  <<< 
// Similar to above but adds the default component extensions for kiosk mode.
 ... } ...  
```
### patch
```
  virtual void AddDefaultComponentExtensions(bool skip_session_components);

```

### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
// Similar to above but adds the default component extensions for kiosk mode.  >>> 
 void AddDefaultComponentExtensionsForKioskMode(bool skip_session_components);  <<< 
// Reloads a registered component extension.
 ... } ...  
```
### patch
```
  virtual void AddDefaultComponentExtensionsForKioskMode(bool skip_session_components);

```

### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
 
 class ComponentLoader : public KeyedService { ...   >>> 
 void 
 AddDefaultComponentExtensionsWithBackgroundPages 
 (  <<< 
bool skip_session_components
 ... ) ...  } ...  } ...  
```
### patch
```
  virtual void AddDefaultComponentExtensionsWithBackgroundPages(

```

### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
virtual void AddDefaultComponentExtensionsWithBackgroundPages(
		bool skip_session_components);  >>> 
 void AddDefaultComponentExtensionsWithBackgroundPagesForKioskMode();  <<< 
#if BUILDFLAG(ENABLE_HANGOUT_SERVICES_EXTENSION)
  void AddHangoutServicesExtension();
#endif
 ... } ...  
```
### patch
```
  virtual void AddDefaultComponentExtensionsWithBackgroundPagesForKioskMode();

```

### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
 
 class ComponentLoader : public KeyedService { ... 
void AddHangoutServicesExtension();
 #endif 
 // BUILDFLAG(ENABLE_HANGOUT_SERVICES_EXTENSION) 
 >>> 
void AddNetworkSpeechSynthesisExtension();
 ... } ...  } ...  
```
### patch
```
  friend class BraveComponentLoader;          

```

