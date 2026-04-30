### match
```cpp
...
 
 >>> 
virtual WebContents* AddNewContents(
      WebContents* source,
      std::unique_ptr<WebContents> new_contents,
      const GURL& target_url,
      WindowOpenDisposition disposition,
      const blink::mojom::WindowFeatures& window_features,
      bool user_gesture,
      bool* was_blocked);
 ...
```
### patch
```cpp
  virtual WebContents* AddNewContents_ChromiumImpl(                                                
      WebContents* source, std::unique_ptr<WebContents> new_contents,
      const GURL& target_url, WindowOpenDisposition disposition,
      const blink::mojom::WindowFeatures& window_features, bool user_gesture,
      bool* was_blocked);

```

