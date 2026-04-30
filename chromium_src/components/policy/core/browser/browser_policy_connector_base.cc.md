### match
```cpp
...
 
 namespace policy { ... 
void BrowserPolicyConnectorBase::OnResourceBundleCreated() {
  std::vector<base::OnceClosure> resource_bundle_callbacks;
  std::swap(resource_bundle_callbacks, resource_bundle_callbacks_);
  for (auto& closure : resource_bundle_callbacks)
    std::move(closure).Run();
}
 } 
 // namespace policy 
 >>> 
 ... 
```
### patch
```cpp
namespace policy {

std::vector<std::unique_ptr<ConfigurationPolicyProvider>>
BrowserPolicyConnectorBase::CreatePolicyProviders_ChromiumImpl() {
  return {};
}

}  // namespace policy
```

