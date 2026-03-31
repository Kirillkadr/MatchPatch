### match
```cpp
...
>>>
 TEST_F(ChromeMetricsServiceClientTest, TestRegisterUKMProviders) 
 {  <<< 
// Test that UKM service has initialized all its metrics providers listed in
 ... } ...  
```
### patch
```cpp
TEST_F(ChromeMetricsServiceClientTest, DISABLED_TestRegisterUKMProviders) {

```

### match
```cpp
...
>>>
 TEST_F(ChromeMetricsServiceClientTest, TestRegisterMetricsServiceProviders) 
 {  <<< 
// This is for the two metrics providers added in the MetricsService
 ... } ...  
```
### patch
```cpp
TEST_F(ChromeMetricsServiceClientTest, DISABLED_TestRegisterMetricsServiceProviders) {

```

### match
```cpp
...
 
 TEST_F(ChromeMetricsServiceClientTest, GetUploadSigningKey_CanSignLogs) { ... 
EXPECT_FALSE(signature.empty());
 } 
 >>> 
 ... 
```
### patch
```cpp
TEST_F(ChromeMetricsServiceClientTest, BraveTestRegisterUKMProviders) {
  std::unique_ptr<ChromeMetricsServiceClient> chrome_metrics_service_client =
      TestChromeMetricsServiceClient::Create(metrics_state_manager_.get(),
                                             synthetic_trial_registry_.get());
  size_t observed_count = chrome_metrics_service_client->GetUkmService()
                              ->metrics_providers_.GetProviders()
                              .size();
  // In Brave, we expect 0 UKM providers regardless of feature flag
  EXPECT_EQ(0ul, observed_count);
}

TEST_F(ChromeMetricsServiceClientTest, BraveRegisterMetricsServiceProviders) {
  std::unique_ptr<TestChromeMetricsServiceClient>
      chrome_metrics_service_client = TestChromeMetricsServiceClient::Create(
          metrics_state_manager_.get(), synthetic_trial_registry_.get());

  // In Brave, we expect only 2 metrics providers (the ones added in the
  // MetricsService constructor)
  EXPECT_EQ(2ul, chrome_metrics_service_client->GetMetricsService()
                     ->GetDelegatingProviderForTesting()
                     ->GetProviders()
                     .size());
}
```

