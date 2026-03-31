### match
```cpp
...
// Ash Internals.  >>> 
 . 
 WithAshInternals 
 (ProfileSelection::kRedirectedToOriginal)  <<<  ...
```
### patch
```cpp
              .WithAshInternals(ProfileSelection::kRedirectedToOriginal).WithRegular(ProfileSelection::kOwnInstance) 
      .WithGuest(ProfileSelection::kOwnInstance)

```

