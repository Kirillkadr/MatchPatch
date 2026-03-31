### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 class WebContents 
 ; 
 >>> 
class RedirectHeuristicTabHelper
    : public WebContentsObserver,
      public WebContentsUserData<RedirectHeuristicTabHelper>,
      public RedirectChainDetector::Observer {
 public:
  ~RedirectHeuristicTabHelper() override;

  CONTENT_EXPORT static std::set<std::string> AllSitesFollowingFirstParty(
      WebContents* web_contents,
      const GURL& first_party_url);

 private:
  explicit RedirectHeuristicTabHelper(WebContents* web_contents);
  // So WebContentsUserData::CreateForWebContents() can call the constructor.
  friend class WebContentsUserData<RedirectHeuristicTabHelper>;

  // Record a RedirectHeuristic event for a cookie access, if eligible. This
  // applies when the tracking site has appeared previously in the current
  // redirect context.
  void MaybeRecordRedirectHeuristic(const ukm::SourceId& first_party_source_id,
                                    const CookieAccessDetails& details);
  void RecordRedirectHeuristic(
      const ukm::SourceId& first_party_source_id,
      const ukm::SourceId& third_party_source_id,
      const CookieAccessDetails& details,
      const size_t sites_passed_count,
      bool is_current_interaction,
      BtmInteractionType interaction_type,
      std::optional<base::Time> last_user_interaction_time);

  // Create all eligible RedirectHeuristic grants for the current redirect
  // chain. This may create a storage access grant for any site in the redirect
  // chain on the last committed site, if it meets the criteria.
  void CreateAllRedirectHeuristicGrants(const GURL& first_party_url);
  void CreateRedirectHeuristicGrant(const GURL& url,
                                    const GURL& first_party_url,
                                    base::TimeDelta grant_duration,
                                    bool has_interaction);

  // Start WebContentsObserver overrides:
  void OnCookiesAccessed(RenderFrameHost* render_frame_host,
                         const CookieAccessDetails& details) override;
  void PrimaryPageChanged(Page& page) override;
  void WebContentsDestroyed() override;

  // Start RedirectChainDetector::Observer overrides:
  void OnNavigationCommitted(NavigationHandle* navigation_handle) override;

  raw_ptr<RedirectChainDetector> detector_;
  raw_ptr<BtmServiceImpl> dips_service_;
  raw_ref<base::Clock> clock_{*base::DefaultClock::GetInstance()};
  std::optional<base::Time> last_commit_timestamp_;

  base::ScopedObservation<RedirectChainDetector,
                          RedirectChainDetector::Observer>
      obs_{this};
  base::WeakPtrFactory<RedirectHeuristicTabHelper> weak_factory_{this};
  WEB_CONTENTS_USER_DATA_KEY_DECL();
}
 ... } ...  
```
### patch
```cpp
#define RedirectHeuristicTabHelper RedirectHeuristicTabHelper_ChromiumImpl

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 class RedirectHeuristicTabHelper
    : public WebContentsObserver,
      public WebContentsUserData<RedirectHeuristicTabHelper>,
      public RedirectChainDetector::Observer { ...   >>> 
 void 
 MaybeRecordRedirectHeuristic 
 ( 
 const ukm::SourceId& first_party_source_id 
 ,  <<< 
const CookieAccessDetails& details
 ... ) ...  } ...  } ...  
```
### patch
```cpp
  void virtual MaybeRecordRedirectHeuristic(const ukm::SourceId& first_party_source_id,

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 class RedirectHeuristicTabHelper
    : public WebContentsObserver,
      public WebContentsUserData<RedirectHeuristicTabHelper>,
      public RedirectChainDetector::Observer { ... 
WEB_CONTENTS_USER_DATA_KEY_DECL();
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
#undef RedirectHeuristicTabHelper

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
#undef RedirectHeuristicTabHelper

 } 
 // namespace content 
 >>> 
 ... 
```
### patch
```cpp
// Disable RedirectHeuristicTabHelper functionality since we disable kBtm, so
// the upstream code would not work (and crash because it doesn't check that
// dips_service_ can be a null).
class RedirectHeuristicTabHelper
    : public content::WebContentsUserData<RedirectHeuristicTabHelper> {
 public:
  CONTENT_EXPORT static std::set<std::string> AllSitesFollowingFirstParty(
      content::WebContents* web_contents,
      const GURL& first_party_url) {
    return {};
  }

 private:
  explicit RedirectHeuristicTabHelper(content::WebContents* web_contents);
  // So WebContentsUserData::CreateForWebContents() can call the constructor.
  friend class content::WebContentsUserData<RedirectHeuristicTabHelper>;
  WEB_CONTENTS_USER_DATA_KEY_DECL();
};

```

