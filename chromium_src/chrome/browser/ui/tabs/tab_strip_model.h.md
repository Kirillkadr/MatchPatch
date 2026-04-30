### match
```cpp
...
#if BUILDFLAG(IS_ANDROID)
#error This file should only be included on desktop.
#endif  >>> 
 class DraggingTabsSession 
 ;  <<< 
class Profile
 ...
```
### patch
```cpp
class DraggingTabsSessionChromium;

```

### match
```cpp
...
 
 class TabStripModel { ...   >>> 
 GetAdjacentTabsAfterSelectedMove 
 ( 
 base::PassKey<DraggingTabsSession> 
 ,  <<< 
int destination_index
 ... ) ...  } ...
```
### patch
```cpp
GetAdjacentTabsAfterSelectedMove(base::PassKey<DraggingTabsSessionChromium>,

```

### match
```cpp
...
 >>> 
 bool IsReadLaterSupportedForAny(const std::vector<int>& indices);  <<< 
// Saves tabs with url supported by Read Later.
 ...
```
### patch
```cpp
virtual bool IsReadLaterSupportedForAny(const std::vector<int>& indices);

```

### match
```cpp
...
 
 class TabStripModel { ... 
 CommandGlicUnshare 
 , 
 >>> 
CommandLast
 ... } ...  
```
### patch
```cpp
    CommandRestoreTab,
    CommandBookmarkAllTabs,
    CommandShowVerticalTabs,
    CommandToggleTabMuted,
    CommandBringAllTabsToThisWindow,
    CommandCloseDuplicateTabs,
    CommandOpenInContainer,
    CommandRenameTab,

```

### match
```cpp
...
 
 class TabStripModel { ...   >>> 
 void 
 SelectRelativeTab 
 ( 
 TabRelativeDirection direction 
 ,  <<< 
TabStripUserGestureDetails detail
 ... ) ...  } ...  
```
### patch
```cpp
  virtual void SelectRelativeTab(TabRelativeDirection direction,

```

### match
```cpp
...
 
 class TabStripModel { ... 
 TabStripUserGestureDetails detail 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
  friend class BraveTabStripModel;

```

