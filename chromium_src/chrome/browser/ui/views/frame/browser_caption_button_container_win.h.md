### match
```cpp
...
>>>
 class 
 BrowserCaptionButtonContainer 
 : 
 public 
 views::View 
 , 
<<< 
...
```
### patch
```cpp
class BrowserCaptionButtonContainer_ChromiumImpl : public views::View,

```

### match
```cpp
...
 
 class BrowserCaptionButtonContainer_ChromiumImpl : public views::View,
public views::WidgetObserver { ... 
>>> 
 METADATA_HEADER(BrowserCaptionButtonContainer, views::View) 
<<< 
...} ...
```
### patch
```cpp
METADATA_HEADER(BrowserCaptionButtonContainer_ChromiumImpl, views::View)

```

### match
```cpp
...
 
 class BrowserCaptionButtonContainer_ChromiumImpl : public views::View,
public views::WidgetObserver { ... 
>>> 
 explicit BrowserCaptionButtonContainer(BrowserFrameViewWin* frame_view); 
 ~BrowserCaptionButtonContainer() override; 
<<< 
// Tests to see if the specified |point| (which is expressed in this view's
 ... ) ...  } ...
```
### patch
```cpp
explicit BrowserCaptionButtonContainer_ChromiumImpl(BrowserFrameViewWin* frame_view);
  ~BrowserCaptionButtonContainer_ChromiumImpl() override;

```

### match
```cpp
...
// See also ClientView::NonClientHitTest.
 int NonClientHitTest(const gfx::Point& point) const; 
 >>> 
 ...
```
### patch
```cpp
friend class BraveBrowserFrameViewWin;

```

### match
```cpp
...
>>> 
base::BindRepeating(&BrowserCaptionButtonContainer::UpdateButtons,
<<< 
 ...
```
### patch
```cpp
base::BindRepeating(&BrowserCaptionButtonContainer_ChromiumImpl::UpdateButtons,

```

### match
```cpp
...
 
 class BrowserCaptionButtonContainer_ChromiumImpl : public views::View,
public views::WidgetObserver { ... 
 } 
 ; 
 >>> 
 ... 
```
### patch
```cpp
class BrowserCaptionButtonContainer
    : public BrowserCaptionButtonContainer_ChromiumImpl {
  METADATA_HEADER(BrowserCaptionButtonContainer,
                  BrowserCaptionButtonContainer_ChromiumImpl)
 public:
  explicit BrowserCaptionButtonContainer(BrowserFrameViewWin* frame_view);
  ~BrowserCaptionButtonContainer() override;

 private:
  const raw_ptr<BrowserFrameViewWin> frame_view_;
};


```

