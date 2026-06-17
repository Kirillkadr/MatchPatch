### match
```cpp
...
 
 namespace translate { ... 
>>> 
 class 
 TranslateUIDelegate 
 { 
<<< 
...} ...  } ...
```
### patch
```cpp
class TranslateUIDelegate_ChromiumImpl {

```

### match
```cpp
...
 
 class TranslateUIDelegate_ChromiumImpl { ... 
>>> 
 TranslateUIDelegate 
 ( 
 const base::WeakPtr<TranslateManager>& translate_manager 
 , 
<<< 
...) ...  } ...
```
### patch
```cpp
TranslateUIDelegate_ChromiumImpl(const base::WeakPtr<TranslateManager>& translate_manager,

```

### match
```cpp
...
 
 namespace translate { ... 
 
 class TranslateUIDelegate_ChromiumImpl { ... 
>>> 
 TranslateUIDelegate(const TranslateUIDelegate&) = delete; 
 TranslateUIDelegate& operator=(const TranslateUIDelegate&) = delete; 
<<< 
...} ...  } ...
```
### patch
```cpp
TranslateUIDelegate_ChromiumImpl(const TranslateUIDelegate_ChromiumImpl&) = delete;
  TranslateUIDelegate_ChromiumImpl& operator=(const TranslateUIDelegate_ChromiumImpl&) = delete;

```

### match
```cpp
...
 
 namespace translate { ... 
 
 class TranslateUIDelegate_ChromiumImpl { ... 
>>> 
 ~TranslateUIDelegate(); 
<<< 
...} ...  } ...
```
### patch
```cpp
  ~TranslateUIDelegate_ChromiumImpl();


```

### match
```cpp
...
 
 namespace translate { ... 
// the language, when we think the user wants that functionality.
>>> 
 bool ShouldShowAlwaysTranslateShortcut() const; 
<<< 
// Returns true if the UI should offer the user a shortcut to never translate
 ... } ...
```
### patch
```cpp
bool virtual ShouldShowAlwaysTranslateShortcut() const;

```

### match
```cpp
...
 
 namespace translate { ... 
// If true, this method has the side effect of mutating some prefs.
>>> 
 bool ShouldAutoAlwaysTranslate(); 
<<< 
// Returns whether "Never Translate Language" should automatically trigger.
 ... } ...
```
### patch
```cpp
bool virtual ShouldAutoAlwaysTranslate();

```

### match
```cpp
...
 
 namespace translate { ...
 >>> 
  } ...
```
### patch
```cpp
class TranslateUIDelegate final : public TranslateUIDelegate_ChromiumImpl {
 public:
  using TranslateUIDelegate_ChromiumImpl::TranslateUIDelegate_ChromiumImpl;
  bool ShouldShowAlwaysTranslateShortcut() const override;
#if BUILDFLAG(IS_ANDROID) || BUILDFLAG(IS_IOS)
  bool ShouldAutoAlwaysTranslate() override;
#endif  // BUILDFLAG(IS_ANDROID) || BUILDFLAG(IS_IOS)
};

```

