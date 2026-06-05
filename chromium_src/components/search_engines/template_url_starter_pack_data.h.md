### match
```cpp
...
 
 namespace template_url_starter_pack_data { ... 

  kNone = 0,

  kBookmarks = 1,
  kHistory = 2,
  kTabs = 3,
  kGemini = 4,
  kPage = 5,
  kAiMode = 6,

  
>>> 
 kMaxStarterPackId 
<<< 
...} ...  
```
### patch
```cpp
  kAskBraveSearch, kMaxStarterPackId

```

### match
```cpp
...
 
 namespace template_url_starter_pack_data { ... 
>>> 
 template_url_starter_pack_data::StarterPackId::kMaxStarterPackId 
 > 
 ; 
<<< 
...} ...  
```
### patch
```cpp
    template_url_starter_pack_data::StarterPackId::kAskBraveSearch, kMaxStarterPackId>;

```

### match
```cpp
...
 
 namespace template_url_starter_pack_data { ... 
// Returns a vector of all starter pack engines, in TemplateURLData format.
>>> 
 std::vector<std::unique_ptr<TemplateURLData>> GetStarterPackEngines(); 
<<< 
// Returns the destination url for the starter pack engine associated with a
 ... } ...  
```
### patch
```cpp
std::vector<std::unique_ptr<TemplateURLData>> GetStarterPackEngines_ChromiumImpl();

```

### match
```cpp
...
 
 namespace template_url_starter_pack_data { ... 
// given starter pack id.
 std::u16string GetDestinationUrlForStarterPackId(StarterPackId id); 
 >>> 
 ... } ...  
```
### patch
```cpp
extern const StarterPackEngine ask_brave_search;
std::vector<std::unique_ptr<TemplateURLData>> GetStarterPackEngines();

```

