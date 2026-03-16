### match
```
...
 
 TEST_F(AidaClientTest, RefetchesTokenWhenExpired) { ... 
EXPECT_NE(authorization_header, delegate.authorization_header_);
 } 
 >>> 
 ... 
```
### patch
```

TEST_F(AidaClientTest, NotAvailable) {
  auto availability = AidaClient::CanUseAida(profile_.get());
  EXPECT_FALSE(availability.available);
  EXPECT_TRUE(availability.blocked);
  EXPECT_TRUE(availability.blocked_by_age);
  EXPECT_TRUE(availability.blocked_by_enterprise_policy);
  EXPECT_TRUE(availability.blocked_by_geo);
  EXPECT_FALSE(availability.blocked_by_rollout);
  EXPECT_TRUE(availability.disallow_logging);
}
```

