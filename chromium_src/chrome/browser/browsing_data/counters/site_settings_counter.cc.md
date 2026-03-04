### match
```
...
#include "chrome/browser/browsing_data/counters/site_settings_counter.h"

 #include "base/json/values_util.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```
#include "brave/components/content_settings/core/browser/brave_content_settings_utils.h"

```

### match
```
...
#include "content/public/browser/host_zoom_map.h"

 #endif 
 >>> 
 ... 
```
### patch
```
namespace {

template <typename Iterator>
void ProcessBraveTypes(Iterator&& iterate_content_settings_list,
                       HostContentSettingsMap* map,
                       int& empty_host_pattern) {
  auto* registry = content_settings::PermissionSettingsRegistry::GetInstance();

  auto fix_empty_host_pattern = [&](ContentSettingsType type) {
    const int saved_empty_host_pattern = empty_host_pattern;
    iterate_content_settings_list(type, map->GetSettingsForOneType(type));
    if (registry->Get(type)) {
      // upstream already counted this type, but empty pattern contains default
      // value, decrease count if it is changed.
      if (empty_host_pattern != saved_empty_host_pattern) {
        empty_host_pattern -=
            2 * (empty_host_pattern - saved_empty_host_pattern);
      }
    } else {
      empty_host_pattern = saved_empty_host_pattern;
    }
  };

  for (const auto type : content_settings::GetShieldsContentSettingsTypes()) {
    fix_empty_host_pattern(type);
  }
  // This is required because we override COOKIES with BRAVE_COOKIES and it's
  // counted twice.
  fix_empty_host_pattern(ContentSettingsType::BRAVE_COOKIES);
}

}  // namespace



```

### match
```
...
 void SiteSettingsCounter::Count() { ... 
for (const auto& exception : tab_discard_exceptions) {
    url_matcher::util::FilterComponents components;
    bool is_valid = url_matcher::util::FilterToComponents(
        exception, &components.scheme, &components.host,
        &components.match_subdomains, &components.port, &components.path,
        &components.query);

    if (is_valid && !components.host.empty()) {
      hosts.insert(components.host);
    } else {
      empty_host_pattern++;
    }
  }  >>> 
 ReportResult(hosts.size() + empty_host_pattern);  <<< ... } ...  
```
### patch
```
  ProcessBraveTypes(iterate_content_settings_list, map_.get(), 
                    empty_host_pattern);
  ReportResult(__VA_ARGS__);

```

