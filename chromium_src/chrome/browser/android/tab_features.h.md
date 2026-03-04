### match
```
...
 # ifndef ... 
 namespace tabs { ...   >>> 
 class 
 TabFeatures 
 {  <<< ... 
public
 ... } ...  } ...  
```
### patch
```
class TabFeatures_Chromium {

```

### match
```
...
 # ifndef ... 
 namespace tabs { ... 
 class TabFeatures_Chromium { ...   >>> 
 TabFeatures(content::WebContents* web_contents, Profile* profile); 
 ~TabFeatures();  <<< ... 
NewTabPagePreloadPipelineManager* new_tab_page_preload_pipeline_manager() {
    return new_tab_page_preload_pipeline_manager_.get();
  }
 ... } ...  } ...  
```
### patch
```
  TabFeatures_Chromium(content::WebContents* web_contents, Profile* profile);
  ~TabFeatures_Chromium();

```

### match
```
...
 # ifndef ... 
 namespace tabs { ... 
 class TabFeatures_Chromium { ... 
std::unique_ptr<glic::GlicSidePanelCoordinator> glic_side_panel_coordinator_;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```
class BraveTabFeatures;
class TabFeatures {
 public:
  TabFeatures(content::WebContents* web_contents, Profile* profile);
  ~TabFeatures();

  NewTabPagePreloadPipelineManager* new_tab_page_preload_pipeline_manager();

 private:
  friend BraveTabFeatures;
  std::unique_ptr<BraveTabFeatures> brave_tab_features_;
};


```

