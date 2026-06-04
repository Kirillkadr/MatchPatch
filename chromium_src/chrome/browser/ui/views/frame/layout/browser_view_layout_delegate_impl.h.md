### match
```cpp
...
 int GetExtraInfobarOffset() const override; 
 >>> 
 ... 
```
### patch
```cpp
  bool ShouldShowVerticalTabs() const override;
  bool IsVerticalTabOnRight() const override;
  bool ShouldUseBraveWebViewRoundedCornersForContents() const override;
  int GetRoundedCornersWebViewMargin() override;
  bool IsBookmarkBarOnByPref() const override;
  bool IsContentTypeSidePanelVisible() override;
  bool IsFullscreenForBrowser() override;                               
  bool IsFullscreenForTab() const override;
  bool IsFullscreen() const override;

```

