### match
```
...
 namespace base { ...   >>> 
 bool 
 FeatureList::IsFeatureOverridden(std::string_view feature_name) const 
 {  <<< ... 
return GetOverrideEntryByFeatureName(feature_name);
 ... } ...  } ...  
```
### patch
```
bool FeatureList::IsFeatureOverridden_ChromiumImpl(std::string_view feature_name) const {

```

### match
```
...
 namespace base { ... 
 bool FeatureList::IsEnabled(const Feature& feature) { ... 
 if (!g_feature_list_instance ||
      !g_feature_list_instance->AllowFeatureAccess(feature)) { ... 
EarlyFeatureAccessTracker::GetInstance()->AccessedFeature(
        feature, g_feature_list_instance &&
                     g_feature_list_instance->IsEarlyAccessInstance());  >>> 
 return feature.default_state == FEATURE_ENABLED_BY_DEFAULT;  <<< ... } ...  } ...  } ...  
```
### patch
```
    return feature.name&& GetCompileTimeFeatureState(feature) == FEATURE_ENABLED_BY_DEFAULT;

```

### match
```
...
 namespace base { ...   >>> 
 std::optional<bool> 
 FeatureList::GetStateIfOverridden(const Feature& feature) 
 {  <<< ... 
if (!g_feature_list_instance ||
      !g_feature_list_instance->AllowFeatureAccess(feature)) {
    EarlyFeatureAccessTracker::GetInstance()->AccessedFeature(
        feature, g_feature_list_instance &&
                     g_feature_list_instance->IsEarlyAccessInstance());
    // If there is no feature list, there can be no overrides.
    return std::nullopt;
  }
 ... } ...  } ...  
```
### patch
```
std::optional<bool> FeatureList::GetStateIfOverridden_ChromiumImpl(const Feature& feature) {

```

### match
```
...
 namespace base { ... 
 bool FeatureList::IsFeatureEnabled(const Feature& feature) const { ... 
if (overridden_state != OVERRIDE_USE_DEFAULT) {
    return overridden_state == OVERRIDE_ENABLE_FEATURE;
  }  >>> 
 return feature.default_state == FEATURE_ENABLED_BY_DEFAULT;  <<< ... } ...  } ...  
```
### patch
```
  return feature.name&& GetCompileTimeFeatureState(feature) == FEATURE_ENABLED_BY_DEFAULT;

```

### match
```
...
 namespace base { ... 
 bool FeatureList::Accessor::GetParamsByFeatureName(
    std::string_view feature_name,
    std::map<std::string, std::string>* params) { ... 
return FieldTrialParamAssociator::GetInstance()->GetFieldTrialParams(trial,
                                                                       params);
 } 
 >>> 
 ... } ...  
```
### patch
```
namespace internal {
namespace {

using DefaultStateOverrides =
    flat_map<std::reference_wrapper<const Feature>, FeatureState>;

using UnsortedDefaultStateOverrides =
    std::vector<DefaultStateOverrides::value_type>;

constexpr size_t kDefaultStateOverridesReserve = 64 * 4;

UnsortedDefaultStateOverrides& GetUnsortedDefaultStateOverrides() {
  static NoDestructor<UnsortedDefaultStateOverrides>
      startup_default_state_overrides([] {
        UnsortedDefaultStateOverrides v;
        v.reserve(kDefaultStateOverridesReserve);
        return v;
      }());
  return *startup_default_state_overrides;
}

const DefaultStateOverrides& GetDefaultStateOverrides() {
  static const NoDestructor<DefaultStateOverrides> kDefaultStateOverrides([] {
    DefaultStateOverrides sorted_overrides =
        std::move(GetUnsortedDefaultStateOverrides());
    DCHECK_EQ(GetUnsortedDefaultStateOverrides().capacity(), 0u);
#if !defined(COMPONENT_BUILD)
    CHECK_GE(kDefaultStateOverridesReserve, sorted_overrides.size())
        << "kDefaultStateOverridesReserve should be increased";
#endif
    return sorted_overrides;
  }());
  return *kDefaultStateOverrides;
}

}  // namespace

FeatureDefaultStateOverrider::FeatureDefaultStateOverrider(
    std::initializer_list<FeatureOverrideInfo> overrides) {
  auto& default_state_overrides = GetUnsortedDefaultStateOverrides();
#if DCHECK_IS_ON()
  {
    flat_set<std::reference_wrapper<const Feature>> new_overrides;
    new_overrides.reserve(overrides.size());
    for (const auto& override : overrides) {
      DCHECK(new_overrides.insert(override.first).second)
          << "Feature " << override.first.get().name
          << " is duplicated in the current override macros";
      DCHECK(!std::ranges::any_of(default_state_overrides,
                                  [&override](const auto& v) {
                                    return &v.first.get() ==
                                           &override.first.get();
                                  }))
          << "Feature " << override.first.get().name
          << " has already been overridden";
    }
  }
#endif
  default_state_overrides.insert(default_state_overrides.end(),
                                 overrides.begin(), overrides.end());
}

}  // namespace internal

// Custom comparator to use std::reference_wrapper as a key in a map/set.
static inline bool operator<(const std::reference_wrapper<const Feature>& lhs,
                             const std::reference_wrapper<const Feature>& rhs) {
  // Compare internal pointers directly, because there must only ever be one
  // struct instance for a given feature name.
  return &lhs.get() < &rhs.get();
}

bool FeatureList::IsFeatureOverridden(std::string_view feature_name) const {
  if (FeatureList::IsFeatureOverridden_ChromiumImpl(feature_name)) {
    return true;
  }

  const auto& default_state_overrides = internal::GetDefaultStateOverrides();
  for (const auto& default_state_override : default_state_overrides) {
    const Feature& feature = default_state_override.first.get();
    if (feature.name == feature_name) {
      return true;
    }
  }
  return false;
}

std::optional<bool> FeatureList::GetStateIfOverridden(const Feature& feature) {
  auto state = GetStateIfOverridden_ChromiumImpl(feature);
  if (state.has_value()) {
    return state;
  }

  const auto& default_state_overrides = internal::GetDefaultStateOverrides();
  const auto default_state_override_it = default_state_overrides.find(feature);
  if (default_state_override_it != default_state_overrides.end()) {
    return default_state_override_it->second ==
           FeatureState::FEATURE_ENABLED_BY_DEFAULT;
  }

  return std::nullopt;
}

// static
FeatureState FeatureList::GetCompileTimeFeatureState(const Feature& feature) {
  const auto& default_state_overrides = internal::GetDefaultStateOverrides();
  const auto default_state_override_it = default_state_overrides.find(feature);
  return default_state_override_it != default_state_overrides.end()
             ? default_state_override_it->second
             : feature.default_state;
}


```

