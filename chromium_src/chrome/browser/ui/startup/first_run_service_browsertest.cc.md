### match
```cpp
...
#include "base/test/scoped_feature_list.h"

 #include "base/test/test_future.h"
 
 >>> 
#include "chrome/browser/browser_process.h"

 ... 
```
### patch
```cpp
#include "brave/grit/brave_generated_resources.h"

```

### match
```cpp
...
#include "testing/gtest/include/gtest/gtest.h"

 #include "ui/base/l10n/l10n_util.h"
 
 >>> 
namespace {
class PolicyUpdateObserver : public policy::PolicyService::Observer {
 public:
  PolicyUpdateObserver(policy::PolicyService& policy_service,
                       base::OnceClosure policy_updated_callback)
      : policy_service_(policy_service),
        policy_updated_callback_(std::move(policy_updated_callback)) {
    DCHECK(policy_updated_callback_);
    policy_service_->AddObserver(policy::PolicyDomain::POLICY_DOMAIN_CHROME,
                                 this);
  }

  ~PolicyUpdateObserver() override {
    policy_service_->RemoveObserver(policy::PolicyDomain::POLICY_DOMAIN_CHROME,
                                    this);
  }

  void OnPolicyUpdated(const policy::PolicyNamespace& ns,
                       const policy::PolicyMap& previous,
                       const policy::PolicyMap& current) override {
    if (ns.domain != policy::PolicyDomain::POLICY_DOMAIN_CHROME) {
      return;
    }

    policy_service_->RemoveObserver(policy::PolicyDomain::POLICY_DOMAIN_CHROME,
                                    this);
    std::move(policy_updated_callback_).Run();
  }

  const raw_ref<policy::PolicyService> policy_service_;
  base::OnceClosure policy_updated_callback_;
};

// Converts JSON string to `base::Value` object.
static base::Value GetJSONAsValue(std::string_view json) {
  std::string error;
  auto value = JSONStringValueDeserializer(json).Deserialize(nullptr, &error);
  EXPECT_EQ("", error);
  return base::Value::FromUniquePtrValue(std::move(value));
}

}
 ... 
```
### patch
```cpp
#define IDS_SIGNIN_DICE_WEB_INTERCEPT_ENTERPRISE_PROFILE_NAME_SAVE \
  IDS_SIGNIN_DICE_WEB_INTERCEPT_ENTERPRISE_PROFILE_NAME
#undef IDS_SIGNIN_DICE_WEB_INTERCEPT_ENTERPRISE_PROFILE_NAME
#define IDS_SIGNIN_DICE_WEB_INTERCEPT_ENTERPRISE_PROFILE_NAME \
  IDS_PROFILE_MENU_BRAVE_PLACEHOLDER_PROFILE_NAME


```

### match
```cpp
...
 
 INSTANTIATE_TEST_SUITE_P ( ... 
 &PolicyParamToTestSuffix 
 ) 
 ; 
 >>> 
 ... 
```
### patch
```cpp

#undef IDS_SIGNIN_DICE_WEB_INTERCEPT_ENTERPRISE_PROFILE_NAME
#define IDS_SIGNIN_DICE_WEB_INTERCEPT_ENTERPRISE_PROFILE_NAME \
  IDS_SIGNIN_DICE_WEB_INTERCEPT_ENTERPRISE_PROFILE_NAME_SAVE
#undef IDS_SIGNIN_DICE_WEB_INTERCEPT_ENTERPRISE_PROFILE_NAME_SAVE
```

