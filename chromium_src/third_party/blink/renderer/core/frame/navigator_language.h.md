### match
```
...
>>>
 class CORE_EXPORT 
 NavigatorLanguage : public 
 GarbageCollectedMixin 
 {  <<< ... 
public:
  explicit NavigatorLanguage(ExecutionContext*);
 ... } ...  
```
### patch
```
class CORE_EXPORT NavigatorLanguage_ChromiumImpl : public GarbageCollectedMixin {

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT NavigatorLanguage_ChromiumImpl : public GarbageCollectedMixin { ...   >>> 
 explicit NavigatorLanguage(ExecutionContext*);  <<< ... } ...  } ...  
```
### patch
```
  explicit NavigatorLanguage_ChromiumImpl(ExecutionContext*);

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT NavigatorLanguage_ChromiumImpl : public GarbageCollectedMixin { ...   >>> 
 void EnsureUpdatedLanguage();  <<< ... } ...  } ...  
```
### patch
```
  void UnusedMethod() {}           \
                              \
 protected:                   \
  virtual void EnsureUpdatedLanguage();

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT NavigatorLanguage_ChromiumImpl : public GarbageCollectedMixin { ... 
bool languages_dirty_ = true;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```
class CORE_EXPORT NavigatorLanguage : public NavigatorLanguage_ChromiumImpl {
 public:
  explicit NavigatorLanguage(ExecutionContext*);
 protected:
  void EnsureUpdatedLanguage() override;
};

```

