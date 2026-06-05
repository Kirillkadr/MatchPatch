### match
```cpp
...
#include <string>

 #include <vector>
 
 >>> 
#include "base/strings/utf_string_conversions.h"

 ... 
```
### patch
```cpp
#include <string_view>
#include "base/strings/strcat.h"
#include "base/strings/string_util.h"
#include "components/grit/brave_components_strings.h"

```

### match
```cpp
...
#include "components/search_engines/template_url_data_util.h"

 #include "components/strings/grit/components_strings.h"
 
 >>> 
namespace template_url_starter_pack_data {

// Update this whenever a change is made to any starter pack data.
const int kCurrentDataVersion = 13;

// Only update this if there's an incompatible change that requires force
// updating the user's starter pack data. This will overwrite any of the
// user's changes to the starter pack entries.
const int kFirstCompatibleDataVersion = 10;

const StarterPackEngine bookmarks = {
    .name_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_BOOKMARKS_NAME,
    .keyword_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_BOOKMARKS_KEYWORD,
    .favicon_url = nullptr,
    .search_url = "chrome://bookmarks/?q={searchTerms}",
    .destination_url = "chrome://bookmarks",
    .id = StarterPackId::kBookmarks,
    .type = SEARCH_ENGINE_STARTER_PACK_BOOKMARKS,
};

const StarterPackEngine history = {
    .name_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_HISTORY_NAME,
    .keyword_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_HISTORY_KEYWORD,
    .favicon_url = nullptr,
    .search_url = "chrome://history/?q={searchTerms}",
    .destination_url = "chrome://history",
    .id = StarterPackId::kHistory,
    .type = SEARCH_ENGINE_STARTER_PACK_HISTORY,
};

const StarterPackEngine tabs = {
    .name_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_TABS_NAME,
    .keyword_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_TABS_KEYWORD,
    .favicon_url = nullptr,
    // This search_url is a placeholder URL to make templateURL happy.
    // chrome://tabs does not currently exist and the tab search engine will
    // only provide suggestions from the OpenTabProvider.
    .search_url = "chrome://tabs/?q={searchTerms}",
    .destination_url = "http://support.google.com/chrome/?p=tab_search",
    .id = StarterPackId::kTabs,
    .type = SEARCH_ENGINE_STARTER_PACK_TABS,
};

const StarterPackEngine gemini = {
    .name_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_GEMINI_NAME,
    .keyword_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_GEMINI_KEYWORD,
    .favicon_url = nullptr,
    .search_url = "https://gemini.google.com/app?q={searchTerms}",
    .destination_url = "https://gemini.google.com",
    .id = StarterPackId::kGemini,
    .type = SEARCH_ENGINE_STARTER_PACK_GEMINI,
};

const StarterPackEngine page = {
    .name_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_PAGE_NAME,
    .keyword_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_PAGE_KEYWORD,
    .favicon_url = nullptr,
    .search_url = "chrome://page/?q={searchTerms}",
    .destination_url = "chrome://page",
    .id = StarterPackId::kPage,
    .type = SEARCH_ENGINE_STARTER_PACK_PAGE,
};

const StarterPackEngine ai_mode = {
    .name_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_AI_MODE_NAME,
    .keyword_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_AI_MODE_KEYWORD,
    .favicon_url = nullptr,
    // - `udm=50` triggers AI mode as opposed to traditional search.
    // - `aep=48` identifies source of the request as the omnibox as opposed to
    //    e.g. the NTP realbox.
    .search_url =
        "https://www.google.com/"
        "search?sourceid=chrome&udm=50&aep=48&q={searchTerms}",
    .destination_url = "https://www.google.com",
    .id = StarterPackId::kAiMode,
    .type = SEARCH_ENGINE_STARTER_PACK_AI_MODE,
};

const StarterPackEngine* engines[] = {
    &bookmarks, &history, &tabs, &gemini, &page, &ai_mode,
};

int GetDataVersion() {
  return kCurrentDataVersion;
}

int GetFirstCompatibleDataVersion() {
  return kFirstCompatibleDataVersion;
}

std::vector<std::unique_ptr<TemplateURLData>> GetStarterPackEngines() {
  std::vector<std::unique_ptr<TemplateURLData>> t_urls;

  for (auto* engine : engines) {
    t_urls.push_back(TemplateURLDataFromStarterPackEngine(*engine));
  }
  return t_urls;
}

std::u16string GetDestinationUrlForStarterPackId(StarterPackId id) {
  for (auto* engine : engines) {
    if (engine->id == id) {
      return base::UTF8ToUTF16(engine->destination_url);
    }
  }

  return u"";
}

}
 ... 
```
### patch
```cpp
namespace {
constexpr char kChromeSchema[] = "chrome://";
constexpr char kBraveSchema[] = "brave://";

}  // namespace

```

### match
```cpp
...
 
 namespace template_url_starter_pack_data { ... 
>>> 
 int 
 GetDataVersion() 
 { 
<<< 
return kCurrentDataVersion;
 ... } ...  } ...  
```
### patch
```cpp
int GetDataVersion_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace template_url_starter_pack_data { ... 
>>> 
 std::vector<std::unique_ptr<TemplateURLData>> 
 GetStarterPackEngines() 
 { 
<<< 
std::vector<std::unique_ptr<TemplateURLData>> t_urls;
 ... } ...  } ...  
```
### patch
```cpp
std::vector<std::unique_ptr<TemplateURLData>> GetStarterPackEngines_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace template_url_starter_pack_data { ... 
>>> 
 std::u16string 
 GetDestinationUrlForStarterPackId(StarterPackId id) 
 { 
<<< 
for (auto* engine : engines) {
    if (engine->id == id) {
      return base::UTF8ToUTF16(engine->destination_url);
    }
  }
 ... } ...  } ...  
```
### patch
```cpp
std::u16string GetDestinationUrlForStarterPackId_ChromiumIml(StarterPackId id) {

```

### match
```cpp
...
 
 namespace template_url_starter_pack_data { ... 
 
 std::u16string GetDestinationUrlForStarterPackId_ChromiumIml(StarterPackId id) { ... 
return u"";
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// Update this whenever a change is made to any Brave-defined starter pack data.
const int kCurrentBraveDataVersion = 1;
const StarterPackEngine ask_brave_search = {
    .name_message_id = IDS_SEARCH_ENGINES_STARTER_PACK_ASK_BRAVE_SEARCH_NAME,
    .keyword_message_id =
        IDS_SEARCH_ENGINES_STARTER_PACK_ASK_BRAVE_SEARCH_KEYWORD,
    .favicon_url = nullptr,
    .search_url = "https://search.brave.com/ask?q={searchTerms}",
    .destination_url = "https://search.brave.com",
    .id = StarterPackId::kAskBraveSearch,
    .type = SEARCH_ENGINE_STARTER_PACK_ASK_BRAVE_SEARCH,
};

const StarterPackEngine* brave_engines[] = {&bookmarks, &history, &tabs,
                                            &ask_brave_search};

int GetDataVersion() {
  return GetDataVersion_ChromiumImpl() + kCurrentBraveDataVersion;
}

std::vector<std::unique_ptr<TemplateURLData>> GetStarterPackEngines() {
  std::vector<std::unique_ptr<TemplateURLData>> t_urls;
  for (auto* engine : brave_engines) {
    auto t_url = TemplateURLDataFromStarterPackEngine(*engine);

    // Replace the "chrome:" scheme in any upstream starter packs.
    std::string_view url(t_url->url());
    if (base::StartsWith(url, kChromeSchema,
                         base::CompareCase::INSENSITIVE_ASCII)) {
      t_url->SetURL(base::StrCat(
          {kBraveSchema, url.substr(std::size(kChromeSchema) - 1)}));
    }

    t_urls.push_back(std::move(t_url));
  }
  return t_urls;
}

std::u16string GetDestinationUrlForStarterPackId(int id) {
  if (id == StarterPackId::kAskBraveSearch) {
    return base::UTF8ToUTF16(ask_brave_search.destination_url);
  }
  return GetDestinationUrlForStarterPackId_ChromiumIml(id);
}

```

