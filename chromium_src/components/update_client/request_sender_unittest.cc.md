### match
```cpp
...
 #include <utility>
 
 >>> 
 ... 
```
### patch
```cpp
#include "base/functional/bind.h"
#include "testing/gtest/include/gtest/gtest.h"

```

### match
```cpp
...
 namespace 
 update_client 
 { 
 >>> 
 ... } ...  
```
### patch
```cpp
class RequestSenderTest;

TEST_F(RequestSenderTest, UsesBraveCUPKey) {
  EXPECT_TRUE(post_interceptor_->ExpectRequest(
      std::make_unique<PartialMatch>("test"),
      GetTestFilePath("updatecheck_reply_1.json")));

  const std::vector<GURL> urls = {GURL(kUrl1)};
  request_sender_ =
      base::MakeRefCounted<RequestSender>(config_->GetNetworkFetcherFactory());
  request_sender_->Send(
      urls, {}, "test", true,
      base::BindOnce(&RequestSenderTest::RequestSenderComplete,
                     base::Unretained(this)));
  RunThreads();

  EXPECT_EQ(1, post_interceptor_->GetHitCount())
      << post_interceptor_->GetRequestsAsString();
  GURL request_url = std::get<2>(post_interceptor_->GetRequests()[0]);
  // It's hard to check the key contents. But it is easy to check the key
  // version. Ours differs from upstream. So we can use this as a proxy check
  // that our key is indeed being used.
  EXPECT_NE(request_url.query().find("cup2key=1:"), std::string::npos)
      << request_url.query();
}

```

