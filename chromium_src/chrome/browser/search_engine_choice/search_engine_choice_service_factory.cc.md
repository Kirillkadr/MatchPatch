### match
```cpp
...
 
 namespace search_engines { ... 
// Ash Internals.  >>> 
 . 
 WithAshInternals 
 (ProfileSelection::kRedirectedToOriginal)  <<<  ...} ...  
```
### patch
```cpp
              .WithAshInternals(ProfileSelection::kRedirectedToOriginal).WithRegular(ProfileSelection::kOwnInstance) 
      .WithGuest(ProfileSelection::kOwnInstance)

```

