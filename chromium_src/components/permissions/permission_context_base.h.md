### match
```cpp
...
 
 # ifndef ... 
 namespace 
 permissions 
 { 
 >>> 
enum class GeolocationPromptType {
  kApproximateOrPrecise,
  kApproximateOnly,
  kUpgradeToPrecise
}
 ... } ...  
```
### patch
```cpp
class PermissionContextBase_ChromiumImpl;
using PermissionContextBase_BraveImpl = PermissionContextBase_ChromiumImpl;
class PermissionLifetimeManager;
class PermissionContextBase : public PermissionContextBase_ChromiumImpl {
 public:
  PermissionContextBase(
      content::BrowserContext* browser_context,
      ContentSettingsType content_settings_type,
      network::mojom::PermissionsPolicyFeature permissions_policy_feature);

  ~PermissionContextBase() override;

  void SetPermissionLifetimeManagerFactory(
      const base::RepeatingCallback<
          PermissionLifetimeManager*(content::BrowserContext*)>& factory);

 private:
  void PermissionDecided(PermissionDecision decision,
                         bool is_final_decision,
                         const PermissionRequestData& request_data) override;

  base::RepeatingCallback<PermissionLifetimeManager*(content::BrowserContext*)>
      permission_lifetime_manager_factory_;
};

```

