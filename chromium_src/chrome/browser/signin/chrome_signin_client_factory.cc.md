### match
```cpp
...
// Ash Internals.  >>> 
 . 
 WithAshInternals 
 (ProfileSelection::kOriginalOnly)  <<<  ...
```
### patch
```cpp
              .WithAshInternals(ProfileSelection::kOriginalOnly) .WithRegular(ProfileSelection::kOwnInstance) 
      .WithGuest(ProfileSelection::kOwnInstance)

```

