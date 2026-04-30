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
class BraveWKWebViewConfigurationProvider
    : public WKWebViewConfigurationProvider {
  using WKWebViewConfigurationProvider::WKWebViewConfigurationProvider;
  void ResetWithWebViewConfiguration(
      WKWebViewConfiguration* configuration) override;
};

```

### match
```cpp
...
   >>> 
 void ResetWithWebViewConfiguration(WKWebViewConfiguration* configuration);  <<< 
// Returns an autoreleased shallow copy of WKWebViewConfiguration associated
 ...
```
### patch
```cpp
void Unused() {}
  virtual void ResetWithWebViewConfiguration(WKWebViewConfiguration* configuration);

```

### match
```cpp
...

 >>> 
std::unique_ptr<WKContentRuleListProvider> content_rule_list_provider_;
  ...
```
### patch
```cpp
friend class BraveWKWebViewConfigurationProvider;

```

