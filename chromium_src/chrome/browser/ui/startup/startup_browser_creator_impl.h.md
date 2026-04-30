### match
```cpp
...
 
 class StartupBrowserCreatorImpl { ...   >>> 
 static 
 void 
 MaybeShowNonMilestoneUpdateToast 
 (  <<< 
Browser* browser
 ... ) ...  } ...  
```
### patch
```cpp
  virtual void MaybeShowNonMilestoneUpdateToast(

```

### match
```cpp
...
raw_ptr<Profile> profile_ = nullptr;
 raw_ptr<StartupBrowserCreator> browser_creator_; 
 >>> 
chrome::startup::IsFirstRun is_first_run_;
 ... 
```
### patch
```cpp
  friend class BraveStartupBrowserCreatorImpl;

```

