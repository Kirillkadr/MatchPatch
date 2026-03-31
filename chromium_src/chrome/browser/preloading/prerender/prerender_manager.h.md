### match
```cpp
...
 
 # ifndef ...   >>> 
 class 
 PrerenderManager 
 : public content::WebContentsObserver,
                         public content::WebContentsUserData<PrerenderManager> 
 {  <<< 
public
 ... } ...  
```
### patch
```cpp
class PrerenderManager_ChromiumImpl : public content::WebContentsObserver,
                         public content::WebContentsUserData<PrerenderManager_ChromiumImpl> {

```

### match
```cpp
...
 
 # ifndef ... 
 
 class PrerenderManager_ChromiumImpl : public content::WebContentsObserver,
                         public content::WebContentsUserData<PrerenderManager_ChromiumImpl> { ...   >>> 
 PrerenderManager(const PrerenderManager&) = delete; 
 PrerenderManager& operator=(const PrerenderManager&) = delete;  <<< 
~PrerenderManager() override;
 ... } ...  
```
### patch
```cpp
  PrerenderManager_ChromiumImpl(const PrerenderManager_ChromiumImpl&) = delete;
  PrerenderManager_ChromiumImpl& operator=(const PrerenderManager_ChromiumImpl&) = delete;

```

### match
```cpp
...
 
 # ifndef ... 
 
 class PrerenderManager_ChromiumImpl : public content::WebContentsObserver,
                         public content::WebContentsUserData<PrerenderManager_ChromiumImpl> { ... 
PrerenderManager_ChromiumImpl& operator=(const PrerenderManager_ChromiumImpl&) = delete;  >>> 
 ~PrerenderManager() override;  <<< 
// content::WebContentsObserver
 ... } ...  
```
### patch
```cpp

  ~PrerenderManager_ChromiumImpl() override;

```

### match
```cpp
...
 
 # ifndef ... 
bool HasSearchResultPagePrerendered() const;  >>> 
 base::WeakPtr<PrerenderManager> GetWeakPtr();  <<< 
// Returns the prerendered search terms if search_prerender_task_ exists.
 ... 
```
### patch
```cpp
  base::WeakPtr<PrerenderManager_ChromiumImpl> GetWeakPtr();

```

### match
```cpp
...
 
 # ifndef ... 
 
 class PrerenderManager_ChromiumImpl : public content::WebContentsObserver,
                         public content::WebContentsUserData<PrerenderManager_ChromiumImpl> { ... 
// LINT.ThenChange(//tools/metrics/histograms/metadata/navigation/enums.xml:PrerenderPrewarmDecision)  >>> 
 explicit PrerenderManager(content::WebContents* web_contents); 
 friend class content::WebContentsUserData<PrerenderManager>;  <<< 
void ResetPrerenderHandlesOnPrimaryPageChanged(
      content::NavigationHandle* navigation_handle);
 ... } ...  
```
### patch
```cpp
  explicit PrerenderManager_ChromiumImpl(content::WebContents* web_contents);
  friend class content::WebContentsUserData<PrerenderManager_ChromiumImpl>;

```

### match
```cpp
...
 
 # ifndef ... 
std::unique_ptr<SearchPrerenderTask> search_prerender_task_;
 std::unique_ptr<content::PrerenderHandle> direct_url_input_prerender_handle_; 
 >>> 
base::WeakPtrFactory<PrerenderManager> weak_factory_{this};
 ... 
```
### patch
```cpp
  base::WeakPtrFactory<PrerenderManager_ChromiumImpl> weak_factory_{this};

  WEB_CONTENTS_USER_DATA_KEY_DECL();
};

class PrerenderManager : public content::WebContentsUserData<PrerenderManager> {
 public:
  PrerenderManager(const PrerenderManager&) = delete;
  PrerenderManager& operator=(const PrerenderManager&) = delete;

  ~PrerenderManager() override;

  // Maybe start prerendering a prewarm page if we haven't prewarm it yet for
  // the underlying WebContents. Returns true if a new prerender is started.
  // TODO(https://crbug.com/423465927): Decide a better timing to close.
  bool MaybeStartPrewarmSearchResult();

  // Deletes the existing prewarm page to start another one for testing.
  void StopPrewarmSearchResultForTesting();

  // Sets the prewarm page URL for testing as it's difficult to set the testing
  // server's URL as a Finch parameter in the tests.
  void SetPrewarmUrlForTesting(const GURL& url);

  // Calling this method will lead to the cancellation of the previous prerender
  // if the given `canonical_search_url` differs from the ongoing one's.
  void StartPrerenderSearchResult(
      const GURL& canonical_search_url,
      const GURL& prerendering_url,
      base::WeakPtr<content::PreloadingAttempt> attempt);

  // Cancels the prerender that is prerendering the given
  // `canonical_search_url`.
  // TODO(crbug.com/40214220): Use the creator's address to identify the
  // owner that can cancels the corresponding prerendering?
  void StopPrerenderSearchResult(const GURL& canonical_search_url);

  // The entry of bookmark prerender.
  // Calling this method will return WeakPtr of the started prerender, and lead
  // to the cancellation of the previous prerender if the given url is different
  // from the on-going one. If the url given is already on-going, this function
  // will return the weak pointer to the on-going prerender handle.
  base::WeakPtr<content::PrerenderHandle> StartPrerenderBookmark(
      const GURL& prerendering_url);
  void StopPrerenderBookmark(
      base::WeakPtr<content::PrerenderHandle> prerender_handle);

  // The entry of new tab page prerender.
  // Calling this method will return WeakPtr of the started prerender, and lead
  // to the cancellation of the previous prerender if the given url is different
  // from the on-going one. If the url given is already on-going, this function
  // will return the weak pointer to the on-going prerender handle.
  base::WeakPtr<content::PrerenderHandle> StartPrerenderNewTabPage(
      const GURL& prerendering_url,
      content::PreloadingPredictor predictor);
  void StopPrerenderNewTabPage(
      base::WeakPtr<content::PrerenderHandle> prerender_handle);

  // The entry of direct url input prerender.
  // Calling this method will return WeakPtr of the started prerender, and lead
  // to the cancellation of the previous prerender if the given url is different
  // from the on-going one. If the url given is already on-going, this function
  // will return the weak pointer to the on-going prerender handle.
  // PreloadingAttempt represents the attempt corresponding to this prerender to
  // log the necessary metrics.
  // TODO(crbug.com/40208255): Merge the start method with DSE interface
  // using AutocompleteMatch as the parameter instead of GURL.
  base::WeakPtr<content::PrerenderHandle> StartPrerenderDirectUrlInput(
      const GURL& prerendering_url,
      content::PreloadingAttempt& preloading_attempt);

  // Returns true if the current tab prerendered a search result for omnibox
  // inputs.
  bool HasSearchResultPagePrerendered() const;

  base::WeakPtr<PrerenderManager> GetWeakPtr();

  // Returns the prerendered search terms if search_prerender_task_ exists.
  // Returns empty string otherwise.
  const GURL GetPrerenderCanonicalSearchURLForTesting() const;

 private:
  explicit PrerenderManager(content::WebContents* web_contents);
  friend class content::WebContentsUserData<PrerenderManager>;


```

