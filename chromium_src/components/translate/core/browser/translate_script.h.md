### match
```cpp
...
 namespace 
 translate 
 { 
 >>> 
 ... } ...
```
### patch
```cpp
class TranslateScript;
using BraveTranslateScript = TranslateScript;

```

### match
```cpp
...
 
 namespace translate { ... 
 class TranslateUrlFetcher 
 ; 
 >>> 
 ... } ...
```
### patch
```cpp
#define TranslateScript ChromiumTranslateScript

```

### match
```cpp
...
 
 namespace translate { ... 
// region preference (which is set by the ChromeDataRegionSetting policy).
>>> 
 void Request(RequestCallback callback, bool is_incognito, PrefService* prefs); 
<<< 
// Returns the URL to be used to load the translate script.
 ... } ...
```
### patch
```cpp
void virtual Request(RequestCallback callback, bool is_incognito, PrefService* prefs);

```

### match
```cpp
...
 
 namespace translate { ... 
// The callback when the script is fetched or a server error occured.
>>> 
 void OnScriptFetchComplete(bool success, const std::string& data); 
<<< 
// URL fetcher to fetch the translate script.
 ... } ...
```
### patch
```cpp
void virtual OnScriptFetchComplete(bool success, const std::string& data);

```

### match
```cpp
...
 
 namespace translate { ... 
 RequestCallbackList callback_list_; 
 >>> 
 ... } ...
```
### patch
```cpp
static GURL AddHostLocaleToUrl(const GURL& url);
  friend BraveTranslateScript;

```

### match
```cpp
...
>>> 
 base::WeakPtrFactory<TranslateScript> weak_method_factory_{this}; 
 } 
 ; 
<<< 
...
```
### patch
```cpp
base::WeakPtrFactory<TranslateScript> weak_method_factory_{this};
  #undef TranslateScript

};
class TranslateScript : public ChromiumTranslateScript {
 public:
  using ChromiumTranslateScript::ChromiumTranslateScript;

  void OnScriptFetchComplete(bool success, const std::string& data) override;
  void Request(RequestCallback callback, bool is_incognito) override;
};

```

