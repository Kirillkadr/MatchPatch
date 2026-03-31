### match
```cpp
...
 
 namespace internal { ... 
 "Prerender.Experimental.PredictionStatus.DirectUrlInput" 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
constexpr char kHistogramPrerenderPredictionStatusDefaultSearchEngine[] =
    "Prerender.Experimental.PredictionStatus.DefaultSearchEngine";
constexpr char kHistogramPrerenderPredictionStatusDirectUrlInput[] =
    "Prerender.Experimental.PredictionStatus.DirectUrlInput";

```

### match
```cpp
...
PrerenderManager::PrerenderManager(content::WebContents* web_contents)
    : content::WebContentsObserver(web_contents),
      content::WebContentsUserData<PrerenderManager>(*web_contents) {}
 WEB_CONTENTS_USER_DATA_KEY_IMPL(PrerenderManager); 
 >>> 
 ... 
```
### patch
```cpp
PrerenderManager::~PrerenderManager() = default;

bool PrerenderManager::MaybeStartPrewarmSearchResult() {
  return false;
}

void PrerenderManager::StopPrewarmSearchResultForTesting() {}

void PrerenderManager::SetPrewarmUrlForTesting(const GURL& url) {}

base::WeakPtr<content::PrerenderHandle>
PrerenderManager::StartPrerenderDirectUrlInput(
    const GURL& prerendering_url,
    content::PreloadingAttempt& preloading_attempt) {
  return nullptr;
}

base::WeakPtr<content::PrerenderHandle>
PrerenderManager::StartPrerenderBookmark(const GURL& prerendering_url) {
  return nullptr;
}

void PrerenderManager::StopPrerenderBookmark(
    base::WeakPtr<content::PrerenderHandle> prerender_handle) {}

base::WeakPtr<content::PrerenderHandle>
PrerenderManager::StartPrerenderNewTabPage(
    const GURL& prerendering_url,
    content::PreloadingPredictor predictor) {
  return nullptr;
}

void PrerenderManager::StopPrerenderNewTabPage(
    base::WeakPtr<content::PrerenderHandle> prerender_handle) {}

void PrerenderManager::StartPrerenderSearchResult(
    const GURL& canonical_search_url,
    const GURL& prerendering_url,
    base::WeakPtr<content::PreloadingAttempt> preloading_attempt) {}

void PrerenderManager::StopPrerenderSearchResult(
    const GURL& canonical_search_url) {}

bool PrerenderManager::HasSearchResultPagePrerendered() const {
  return false;
}

base::WeakPtr<PrerenderManager> PrerenderManager::GetWeakPtr() {
  return weak_factory_.GetWeakPtr();
}

const GURL PrerenderManager::GetPrerenderCanonicalSearchURLForTesting() const {
  return GURL();
}

PrerenderManager::PrerenderManager(content::WebContents* web_contents)
    : content::WebContentsUserData<PrerenderManager>(*web_contents) {}

WEB_CONTENTS_USER_DATA_KEY_IMPL(PrerenderManager);
```

