### match
```cpp
...
 NS_ASSUME_NONNULL_END 
 >>> 
 ... 
```
### patch
```cpp
// Helper category to expose the underlying `PersonalDataManager` so it may be
// used in //brave/ios/web_view targets to expose functionality missing from
// CWVAutofillDataManager
@interface CWVAutofillDataManager (Internal)
- (autofill::PersonalDataManager*)personalDataManager;

@end

```

