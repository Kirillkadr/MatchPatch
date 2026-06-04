### match
```cpp
...
 virtual int GetExtraInfobarOffset() const = 0; 
 >>> 
 ... 
```
### patch
```cpp
  virtual bool ShouldShowVerticalTabs() const = 0;
  virtual bool IsVerticalTabOnRight() const = 0;
  virtual bool ShouldUseBraveWebViewRoundedCornersForContents() const = 0;
  virtual int GetRoundedCornersWebViewMargin() = 0;
  virtual bool IsBookmarkBarOnByPref() const = 0;
  virtual bool IsContentTypeSidePanelVisible() = 0;
  virtual bool IsFullscreenForBrowser() = 0;
  virtual bool IsFullscreenForTab() const = 0;
  virtual bool IsFullscreen() const = 0;

```

