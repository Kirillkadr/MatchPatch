### match
```cpp
...
bool IsSearchByImageAvailable(JNIEnv* env);
>>> 
 bool DoesDefaultSearchEngineHaveLogo(JNIEnv* env); 
<<< 
bool IsDefaultSearchEngineGoogle(JNIEnv* env);
 ... 
```
### patch
```cpp
  bool DoesDefaultSearchEngineHaveLogo_ChromiumImpl(JNIEnv* env); 
  jboolean DoesDefaultSearchEngineHaveLogo(JNIEnv* env);

```

