### match
```
...
// found in the LICENSE file.
 #include "chrome/browser/feed/rss_links_fetcher.h"
 
 >>> 
#include "base/test/metrics/histogram_tester.h"

 ... 
```
### patch
```
#include "base/metrics/histogram_base.h"

```

### match
```
...
#else
#include "chrome/test/base/in_process_browser_test.h"

 #endif 
 >>> 
 ... 
```
### patch
```
namespace base {
namespace {
class HistogramTesterStub {
 public:
  HistogramTesterStub() = default;
  ~HistogramTesterStub() = default;

  void ExpectTotalCount(StringPiece name, HistogramBase::Count count) const {}
};
}  // namespace
}  // namespace base


```

### match
```
...
 
 namespace { ... 
 
 class RssLinksFetcherTest : public AndroidBrowserTest { ... 
 
 IN_PROC_BROWSER_TEST_F(RssLinksFetcherTest, FetchSuccessfulFromHead) { ... 
ASSERT_TRUE(content::NavigateToURL(web_contents, url));  >>> 
 base::HistogramTester histogram_tester;  <<< 
CallbackReceiver<std::vector<GURL>> rss_links;
 ... } ...  } ...  } ...  
```
### patch
```
  base::HistogramTesterStub histogram_tester;

```

### match
```
...
 
 namespace { ... 
 
 class RssLinksFetcherTest : public AndroidBrowserTest { ... 
 
 IN_PROC_BROWSER_TEST_F(RssLinksFetcherTest, FetchSuccessfulFromBody) { ... 
ASSERT_TRUE(content::NavigateToURL(web_contents, url));  >>> 
 base::HistogramTester histogram_tester;  <<< 
CallbackReceiver<std::vector<GURL>> rss_links;
 ... } ...  } ...  } ...  
```
### patch
```
  base::HistogramTesterStub histogram_tester;

```

