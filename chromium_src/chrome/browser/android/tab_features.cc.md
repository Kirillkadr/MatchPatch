### match
```
...
 namespace tabs { ...   >>> 
 TabFeatures::TabFeatures(content::WebContents* web_contents, Profile* profile) 
 {  <<< ... 
sync_sessions_router_ =
      std::make_unique<sync_sessions::SyncSessionsRouterTabHelper>(
          web_contents,
          sync_sessions::SyncSessionsWebContentsRouterFactory::GetForProfile(
              profile),
          ChromeTranslateClient::FromWebContents(web_contents),
          favicon::ContentFaviconDriver::FromWebContents(web_contents));
 ... } ...  } ...  
```
### patch
```
TabFeatures_Chromium::TabFeatures_Chromium(content::WebContents* web_contents, Profile* profile) {

```

### match
```
...
 namespace tabs { ... 
TabFeatures_Chromium::TabFeatures_Chromium(content::WebContents* web_contents, Profile* profile) {
	sync_sessions_router_ =
      std::make_unique<sync_sessions::SyncSessionsRouterTabHelper>(
          web_contents,
          sync_sessions::SyncSessionsWebContentsRouterFactory::GetForProfile(
              profile),
          ChromeTranslateClient::FromWebContents(web_contents),
          favicon::ContentFaviconDriver::FromWebContents(web_contents));

  if (base::FeatureList::IsEnabled(net::features::kVerifyQWACs)) {
    qwac_web_contents_observer_ =
        std::make_unique<QwacWebContentsObserver>(web_contents);
  }

  new_tab_page_preload_pipeline_manager_ =
      std::make_unique<NewTabPagePreloadPipelineManager>(web_contents);

  TabInterface* const tab = TabInterface::GetFromContents(web_contents);
  if (base::FeatureList::IsEnabled(features::kGlicActor)) {
    actor_tab_data_ =
        GetUserDataFactory().CreateInstance<actor::ActorTabData>(*tab, tab);
  }
  tab_contextualization_controller_ =
      GetUserDataFactory().CreateInstance<lens::TabContextualizationController>(
          *tab, tab);

  glic_instance_helper_ =
      GetUserDataFactory().CreateInstance<glic::GlicInstanceHelper>(*tab, tab);
  glic_side_panel_coordinator_ =
      GetUserDataFactory()
          .CreateInstance<glic::GlicSidePanelCoordinatorAndroid>(*tab, tab);
}  >>> 
 TabFeatures::~TabFeatures() = default;  <<< ... 
// static
 ... } ...  
```
### patch
```
TabFeatures_Chromium::~TabFeatures_Chromium() = default;

```

### match
```
...
 namespace tabs { ...   >>> 
 ui::UserDataFactoryWithOwner<TabInterface> 
 & TabFeatures::GetUserDataFactory() 
 {  <<< ... 
static base::NoDestructor<ui::UserDataFactoryWithOwner<TabInterface>> factory;
 ... } ...  } ...  
```
### patch
```
ui::UserDataFactoryWithOwner<TabInterface>& TabFeatures_Chromium::GetUserDataFactory() {

```

