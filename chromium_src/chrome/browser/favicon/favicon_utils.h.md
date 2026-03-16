### match
```
...
 
 # ifndef ... 
 
 namespace favicon { ... 
// Return true if the favicon for |entry| should be themified, based on both
 // its visible and actual URL. 
 >>> 
bool ShouldThemifyFaviconForEntry(content::NavigationEntry* entry);
 ... } ...  
```
### patch
```
bool ShouldThemifyFaviconForEntry_ChromiumImpl(content::NavigationEntry* entry);

```

