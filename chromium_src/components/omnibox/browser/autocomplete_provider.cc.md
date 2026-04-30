### match
```cpp
...
 
 const char* AutocompleteProvider::TypeToString(Type type) { ... 
 switch 
 (type) 
 { 
 >>> 
case TYPE_BOOKMARK:
      return "Bookmark";
 ... } ...  } ...  
```
### patch
```cpp
    case TYPE_BRAVE_COMMANDER:
  case TYPE_BRAVE_LEO:

```

### match
```cpp
...
 
 metrics::OmniboxEventProto_ProviderType
AutocompleteProvider::AsOmniboxEventProviderType() const { ... 
 switch 
 (type_) 
 { 
 >>> 
case TYPE_BOOKMARK:
      return metrics::OmniboxEventProto::BOOKMARK;
 ... } ...  } ...  
```
### patch
```cpp
    case TYPE_BRAVE_COMMANDER: 
  case TYPE_BRAVE_LEO:

```

