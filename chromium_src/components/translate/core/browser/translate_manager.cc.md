### match
```cpp
...
 
 namespace translate { ... 
 
 bool TranslateManager::CanManuallyTranslate(bool menuLogging) { ... 
 if ( ... 
>>> 
 !::google_apis::HasAPIKeyConfigured() 
 ) 
 { 
<<< 
...} ...  } ...  } ...  
```
### patch
```cpp
      !::google_apis::BraveHasAPIKeyConfigured()) {

```

### match
```cpp
...
 
 namespace translate { ... 
 
 bool TranslateManager::IsAvailable(const TranslatePrefs* prefs) { ... 
>>> 
 ::google_apis::HasAPIKeyConfigured() 
 ) 
 && 
<<< 
...} ...  } ...  
```
### patch
```cpp
          ::google_apis::BraveHasAPIKeyConfigured()) &&

```

### match
```cpp
...
 
 namespace translate { ... 
 
 void TranslateManager::FilterIsTranslatePossible(
    TranslateTriggerDecision* decision,
    TranslatePrefs* translate_prefs,
    std::string_view page_language_code,
    std::string_view target_lang) { ... 
 if ( ... 
>>> 
 !::google_apis::HasAPIKeyConfigured() 
 ) 
 { 
<<< 
// Without an API key, translate won't work, so don't offer to translate in
 ... } ...  } ...  } ...  
```
### patch
```cpp
      !::google_apis::BraveHasAPIKeyConfigured()) {

```

