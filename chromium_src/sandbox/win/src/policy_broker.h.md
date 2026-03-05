### match
```
...
 # ifndef ... 
 namespace 
 sandbox 
 { 
 >>> 
class TargetProcess
 ... } ...  
```
### patch
```
class TargetConfig;

```

### match
```
...
>>>
 bool 
 SetupBasicInterceptions 
 ( 
 InterceptionManager* manager 
 ,  <<< ... 
bool is_csrss_connected
 ... ) ...  
```
### patch
```
bool SetupBasicInterceptions_ChromiumImpl(InterceptionManager* manager,

```

### match
```
...
 # ifndef ... 
 namespace sandbox { ... 
 bool is_csrss_connected 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```
  bool SetupBasicInterceptions(InterceptionManager* manager,
                             bool is_csrss_connected, const TargetConfig* config);

```

