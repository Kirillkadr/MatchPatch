### match
```
...
 
 # ifndef ...   >>> 
 class 
 DownloadDisplayController 
 : 
 public 
 FullscreenObserver 
 ,  <<< 
public
 ...
```
### patch
```
class DownloadDisplayControllerChromium : public FullscreenObserver,

```

### match
```
...
class DownloadDisplayControllerChromium : public FullscreenObserver,
                                  public base::PowerSuspendObserver {
 public:  >>> 
 DownloadDisplayController 
 ( 
 DownloadDisplay* display 
 ,  <<< 
Browser* browser
 ... ) ...  }
```
### patch
```
  DownloadDisplayControllerChromium(DownloadDisplay* display,

```

### match
```
...
 
 # ifndef ... 
DownloadDisplayControllerChromium(DownloadDisplay* display,
	Browser* browser,
                            DownloadBubbleUIController* bubble_controller);  >>> 
 DownloadDisplayController(const DownloadDisplayController&) = delete; 
 DownloadDisplayController 
 & operator=(const DownloadDisplayController&) 
 =  <<<  ...
```
### patch
```
  DownloadDisplayControllerChromium(const DownloadDisplayControllerChromium&) = delete;
  DownloadDisplayControllerChromium& operator=(const DownloadDisplayControllerChromium&) =

```

### match
```
...
 
 # ifndef ... 
 
 class DownloadDisplayControllerChromium : public FullscreenObserver,
public base::PowerSuspendObserver { ... 
DownloadDisplayControllerChromium& operator=(const DownloadDisplayControllerChromium&) =
	delete;  >>> 
 ~DownloadDisplayController() override;  <<< 
// Notifies the controller that the button is pressed. Called by `display_`.
 ... } ...  
```
### patch
```
  ~DownloadDisplayControllerChromium() override;

```

### match
```
...
 
 # ifndef ... 
void OpenSecuritySubpage(const offline_items_collection::ContentId& id);  >>> 
 private 
 :  <<< 
friend class DownloadDisplayControllerTest;
 ... 
```
### patch
```
 protected:

```

### match
```
...
 
 # ifndef ... 
 
 class DownloadDisplayControllerChromium : public FullscreenObserver,
public base::PowerSuspendObserver { ...   >>> 
 void 
 UpdateToolbarButtonState 
 (  <<< 
const DownloadBubbleDisplayInfo& info
 ... ) ...  } ...  
```
### patch
```
  virtual void UpdateToolbarButtonState(

```

### match
```
...
 
 # ifndef ... 
raw_ptr<DownloadBubbleUIController, DanglingUntriaged> bubble_controller_;  >>> 
 base::WeakPtrFactory<DownloadDisplayController> weak_factory_{this};  <<<  ...
```
### patch
```
  base::WeakPtrFactory<DownloadDisplayControllerChromium> weak_factory_{this};

```

### match
```
...
 #endif 
 // CHROME_BROWSER_DOWNLOAD_BUBBLE_DOWNLOAD_DISPLAY_CONTROLLER_H_ 
 >>> 
 ... 
```
### patch
```

class DownloadDisplayController : public DownloadDisplayControllerChromium {
 public:
  using DownloadDisplayControllerChromium::DownloadDisplayControllerChromium;

 private:
  void UpdateToolbarButtonState(
      const DownloadBubbleDisplayInfo& info,
      const DownloadDisplay::ProgressInfo& progress_info) override;
};
```

