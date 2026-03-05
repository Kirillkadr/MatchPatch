### match
```
...
 namespace network::features { ... 
 >>> } ...
```
### patch
```
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kBrowsingTopics, base::FEATURE_DISABLED_BY_DEFAULT},
    {kInterestGroupStorage, base::FEATURE_DISABLED_BY_DEFAULT},
    {kLocalNetworkAccessChecksWebSockets, base::FEATURE_ENABLED_BY_DEFAULT},
    {kSharedStorageAPI, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```
