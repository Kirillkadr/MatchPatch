### match
```cpp
...
#include <utility>

 #include "base/functional/bind.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/components/brave_perf_predictor/browser/perf_predictor_page_metrics_observer.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 bool PageLoadMetricsEmbedder::ShouldObserveScheme(std::string_view scheme) { ... 
// BUILDFLAG(IS_CHROMEOS)
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
class BravePageLoadMetricsEmbedder : public PageLoadMetricsEmbedder {
 public:
  explicit BravePageLoadMetricsEmbedder(content::WebContents* web_contents);
  BravePageLoadMetricsEmbedder(const BravePageLoadMetricsEmbedder&) = delete;
  BravePageLoadMetricsEmbedder& operator=(const BravePageLoadMetricsEmbedder&) =
      delete;
  ~BravePageLoadMetricsEmbedder() override;

 protected:
  // page_load_metrics::PageLoadMetricsEmbedderBase:
  void RegisterObservers(page_load_metrics::PageLoadTracker* tracker,
                         content::NavigationHandle* navigation_handle) override;
};

BravePageLoadMetricsEmbedder::BravePageLoadMetricsEmbedder(
    content::WebContents* web_contents)
    : PageLoadMetricsEmbedder(web_contents) {}

BravePageLoadMetricsEmbedder::~BravePageLoadMetricsEmbedder() = default;

void BravePageLoadMetricsEmbedder::RegisterObservers(
    page_load_metrics::PageLoadTracker* tracker,
    content::NavigationHandle* navigation_handle) {
  PageLoadMetricsEmbedder::RegisterObservers(tracker, navigation_handle);

  tracker->AddObserver(
      std::make_unique<
          brave_perf_predictor::PerfPredictorPageMetricsObserver>());
}


```

### match
```cpp
...
>>>
 void 
 InitializePageLoadMetricsForWebContents 
 (  <<< 
content::WebContents* web_contents
 ... ) ...  
```
### patch
```cpp
void InitializePageLoadMetricsForWebContents_Chromium(

```

### match
```cpp
...
 
 void InitializePageLoadMetricsForWebContents_Chromium(
content::WebContents* web_contents) { ... 
page_load_metrics::MetricsWebContentsObserver::CreateForWebContents(
      web_contents, std::make_unique<PageLoadMetricsEmbedder>(web_contents));
 } 
 >>> 
 ... 
```
### patch
```cpp
void InitializePageLoadMetricsForWebContents(
    content::WebContents* web_contents) {
  // TODO(bug https://github.com/brave/brave-browser/issues/7784)
  // change
  // android_webview/browser/page_load_metrics/page_load_metrics_initialize.cc
  // as well to register Page Load Metrics Observers
  page_load_metrics::MetricsWebContentsObserver::CreateForWebContents(
      web_contents,
      std::make_unique<BravePageLoadMetricsEmbedder>(web_contents));
}
```

