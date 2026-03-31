### match
```cpp
...
 
 # ifndef ...   >>> 
 class 
 StubResolverConfigReader 
 {  <<< 
public
 ... } ...
```
### patch
```cpp
class StubResolverConfigReader_ChromiumImpl {

```

### match
```cpp
...
 
 >>> 
 explicit 
 StubResolverConfigReader 
 ( 
 PrefService* local_state 
 ,  <<< 
bool set_up_pref_defaults = true
 ... ) ...
```
### patch
```cpp
explicit StubResolverConfigReader_ChromiumImpl(PrefService* local_state,

```

### match
```cpp
...
 

 
  
explicit StubResolverConfigReader_ChromiumImpl(PrefService* local_state,
bool set_up_pref_defaults = true);  >>> 
 StubResolverConfigReader(const StubResolverConfigReader&) = delete; 
 StubResolverConfigReader& operator=(const StubResolverConfigReader&) = delete;  <<< 
virtual ~StubResolverConfigReader();
 ...
```
### patch
```cpp
StubResolverConfigReader_ChromiumImpl(const StubResolverConfigReader_ChromiumImpl&) = delete;
  StubResolverConfigReader_ChromiumImpl& operator=(const StubResolverConfigReader_ChromiumImpl&) = delete;

```

### match
```cpp
...

StubResolverConfigReader_ChromiumImpl& operator=(const StubResolverConfigReader_ChromiumImpl&) = delete;  >>> 
 virtual ~StubResolverConfigReader();  <<< 
static void RegisterPrefs(PrefRegistrySimple* registry);
 ...
```
### patch
```cpp
  virtual ~StubResolverConfigReader_ChromiumImpl();


```

### match
```cpp
...
 
 # ifndef ... 
#if BUILDFLAG(IS_WIN)
  // Flag used for testing Zero Trust DNS scenario.
  static bool is_ztdns_enabled_for_testing_;
#endif  >>> 
 base::WeakPtrFactory<StubResolverConfigReader> weak_factory_{this};  <<<  ...
```
### patch
```cpp
  base::WeakPtrFactory<StubResolverConfigReader_ChromiumImpl> weak_factory_{this};

```

### match
```cpp
...
 #endif 
 // CHROME_BROWSER_NET_STUB_RESOLVER_CONFIG_READER_H_ 
 >>> 
 ... 
```
### patch
```cpp

class StubResolverConfigReader : public StubResolverConfigReader_ChromiumImpl {
 public:
  explicit StubResolverConfigReader(PrefService* local_state,
                                    bool set_up_pref_defaults = true)
      : StubResolverConfigReader_ChromiumImpl(local_state,
                                              set_up_pref_defaults) {}
  bool ShouldDisableDohForManaged() override;
};

```

