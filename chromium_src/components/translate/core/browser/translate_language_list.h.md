### match
```cpp
...
 
 namespace translate { ... 
>>> 
 class 
 TranslateLanguageList 
 { 
<<< 
...} ...  } ...
```
### patch
```cpp
class TranslateLanguageList_ChromiumImpl {

```

### match
```cpp
...
 
 namespace translate { ... 
 
 class TranslateLanguageList_ChromiumImpl { ... 
// The empty constructor will create the default TranslateUrlFetcher.
>>> 
 TranslateLanguageList(); 
 explicit TranslateLanguageList(std::unique_ptr<TranslateUrlFetcher> fetcher); 
<<< 
...} ...  } ...
```
### patch
```cpp
TranslateLanguageList_ChromiumImpl();
  explicit TranslateLanguageList_ChromiumImpl(std::unique_ptr<TranslateUrlFetcher> fetcher);

```

### match
```cpp
...
 
 namespace translate { ... 
 
 class TranslateLanguageList_ChromiumImpl { ... 
>>> 
 TranslateLanguageList(const TranslateLanguageList&) = delete; 
 TranslateLanguageList& operator=(const TranslateLanguageList&) = delete; 
 virtual ~TranslateLanguageList(); 
<<< 
// Returns the last-updated time when the language list is fetched from the
 ... } ...  } ...
```
### patch
```cpp
TranslateLanguageList_ChromiumImpl(const TranslateLanguageList_ChromiumImpl&) = delete;
  TranslateLanguageList_ChromiumImpl& operator=(const TranslateLanguageList_ChromiumImpl&) = delete;

  virtual ~TranslateLanguageList_ChromiumImpl();

```

### match
```cpp
...
 
 namespace translate { ... 
// pending request.
>>> 
 void SetResourceRequestsAllowed(bool allowed); 
<<< 
...} ...
```
### patch
```cpp
void virtual SetResourceRequestsAllowed(bool allowed);

```

### match
```cpp
...
 
 namespace translate { ... 
 >>>  } ...
```
### patch
```cpp
class TranslateLanguageList : public TranslateLanguageList_ChromiumImpl {
 public:
  void SetResourceRequestsAllowed(bool allowed) override;
};

```

