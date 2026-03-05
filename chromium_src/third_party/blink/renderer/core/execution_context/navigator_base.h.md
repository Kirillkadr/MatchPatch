### match
```
...
 # ifndef ... 
 namespace blink { ... 
class CORE_EXPORT NavigatorBase : public ScriptWrappable,
                                  public NavigatorConcurrentHardware,
                                  public NavigatorDeviceMemory,
                                  public NavigatorID,
                                  public NavigatorLanguage,
                                  public NavigatorOnLine,
                                  public NavigatorUA,
                                  public ExecutionContextClient,
                                  public Supplementable<NavigatorBase> {
 public:
  explicit NavigatorBase(ExecutionContext* context);
 // NavigatorID override 
 >>> 
String userAgent() const override;
 ... } ...  } ...  
```
### patch
```
  String userAgent_ChromiumImpl() const;

```

