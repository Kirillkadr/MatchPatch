### match
```cpp
...
 
 # ifndef ... 
 
 namespace bookmarks::prefs { ... 
// Boolean which specifies whether the bookmark bar is visible on all tabs.
 inline constexpr char kShowBookmarkBar[] = "bookmark_bar.show_on_all_tabs"; 
 >>> 
 ... } ...  
```
### patch
```cpp
inline constexpr char kAlwaysShowBookmarkBarOnNTP[] =
    "brave.always_show_bookmark_bar_on_ntp";

```

