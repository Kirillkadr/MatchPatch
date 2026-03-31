### match
```cpp
... >>> 
void SortAndCull(const AutocompleteInput& input,
                   TemplateURLService* template_url_service,
                   OmniboxTriggeredFeatureService* triggered_feature_service,
                   bool is_lens_active,
                   bool can_show_contextual_suggestions,
                   bool mia_enabled,
                   bool is_incognito,
                   std::optional<AutocompleteMatch> default_match_to_preserve =
                       std::nullopt);
 ...
```
### patch
```cpp
  void Unused();                                                   
  void RemoveAllMatchesNotOfType(AutocompleteProvider::Type); 
  template <typename UnaryPredicate>                          
  void MoveMatchToBeLast(UnaryPredicate predicate) {          
    if (auto it = std::ranges::find_if(matches_, predicate);  
        it != matches_.end()) {                               
      std::rotate(it, std::next(it), matches_.end());         
    }                                                         
  }                                                           

```

### match
```cpp
...
 
 # ifndef ... 
//   afterwards is probably invalid.  >>> 
 void Unused(); 
 void RemoveAllMatchesNotOfType(AutocompleteProvider::Type); 
 template <typename UnaryPredicate>                          
  void MoveMatchToBeLast(UnaryPredicate predicate) {          
    if (auto it = std::ranges::find_if(matches_, predicate);  
        it != matches_.end()) {                               
      std::rotate(it, std::next(it), matches_.end());         
    }                                                         
  }  <<< 
void SortAndCull(const AutocompleteInput& input,
                   TemplateURLService* template_url_service,
                   OmniboxTriggeredFeatureService* triggered_feature_service,
                   bool is_lens_active,
                   bool can_show_contextual_suggestions,
                   bool mia_enabled,
                   bool is_incognito,
                   std::optional<AutocompleteMatch> default_match_to_preserve =
                       std::nullopt);
 ... 
```
### patch
```cpp
  void Unused();                                                   \
  void RemoveAllMatchesNotOfType(AutocompleteProvider::Type); \
  template <typename UnaryPredicate>                          \
  void MoveMatchToBeLast(UnaryPredicate predicate) {          \
    if (auto it = std::ranges::find_if(matches_, predicate);  \
        it != matches_.end()) {                               \
      std::rotate(it, std::next(it), matches_.end());         \
    }                                                         \
  }                                                           \

```

