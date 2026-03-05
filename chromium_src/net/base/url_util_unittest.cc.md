### match
``` ... 
for (const auto& host : test_cases) {
    EXPECT_EQ(host.expected_output, IsGoogleHostWithAlpnH3(host.host));
  }
 } 
 >>> 
 ... 
```
### patch
```
TEST(UrlUtilTest, IsOnionOrigin) {
  EXPECT_TRUE(IsOnion(url::Origin::Create(GURL("https://foo.onion/"))));
  EXPECT_TRUE(IsOnion(url::Origin::Create(GURL("https://foo.onion:20000/"))));
  EXPECT_TRUE(IsOnion(url::Origin::Create(GURL("https://foo.bar.onion/"))));
  EXPECT_FALSE(IsOnion(url::Origin::Create(GURL("https://foo.onion.com/"))));
  EXPECT_FALSE(IsOnion(url::Origin::Create(GURL("https://foo.com/b.onion"))));
}
TEST(UrlUtilTest, IsOnionUrlSchemes) {
  EXPECT_TRUE(IsOnion(GURL("https://foo.onion/")));
  EXPECT_TRUE(IsOnion(GURL("Http://foo.bar.onion/")));
  EXPECT_TRUE(IsOnion(GURL("wSs://foo.onion/bar")));
  EXPECT_TRUE(IsOnion(GURL("WS://foo.onion/bar")));
  EXPECT_FALSE(IsOnion(GURL("file:///foo.onion/bar")));
  EXPECT_FALSE(IsOnion(GURL("ftp://foo.onion/")));
  EXPECT_FALSE(IsOnion(GURL("data:,foo.onion")));
  EXPECT_FALSE(IsOnion(GURL("chrome://onion/")));
}

```

