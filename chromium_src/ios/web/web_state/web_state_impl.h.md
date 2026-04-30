### match
```cpp
...
 
 # ifndef ... 
 namespace 
 web 
 { 
 >>> 
class BrowserState
 ... } ...
```
### patch
```cpp
class WebUIIOS;

```

### match
```cpp
...

 void ClearWebUI(); 
 >>> 
 ...
```
### patch
```cpp
web::WebUIIOS* GetMainFrameWebUI();
  size_t GetWebUICountForTesting();

```

