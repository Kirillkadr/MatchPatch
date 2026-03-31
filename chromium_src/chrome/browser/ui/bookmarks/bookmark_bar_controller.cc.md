### match
```cpp
...
#include "components/tabs/public/split_tab_data.h"

 #include "components/tabs/public/tab_interface.h"
 
 >>> 
#include "content/public/browser/navigation_entry.h"

 ... 
```
### patch
```cpp
#include "components/user_prefs/user_prefs.h"
#include "content/public/browser/browser_context.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 bool IsShowingNTP(content::WebContents* web_contents) { ...   >>> 
 if 
 (SadTab::ShouldShow(web_contents->GetCrashedStatus())) 
 {  <<< 
return false;
 ... } ...  } ...  } ...  
```
### patch
```cpp
  if (SadTab:: ShouldShow(web_contents->GetCrashedStatus()) || !ShowBookmarkBarEnabled(web_contents)) {

```

### match
```cpp
...
 
 namespace { ... 
 
 bool IsShowingNTP(content::WebContents* web_contents) { ... 
 
 if (SadTab:: ShouldShow(web_contents->GetCrashedStatus()) || !ShowBookmarkBarEnabled(web_contents)) { ... 
return false;
 } 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
bool ShowBookmarkBarEnabled(content::WebContents* web_contents) {
  PrefService* prefs =
      user_prefs::UserPrefs::Get(web_contents->GetBrowserContext());
  return prefs->GetBoolean(::bookmarks::prefs::kAlwaysShowBookmarkBarOnNTP) ||
         prefs->GetBoolean(::bookmarks::prefs::kShowBookmarkBar);
}


```

### match
```cpp
...
 
 bool BookmarkBarController::ShouldShowBookmarkBar() const { ... 
bookmarks::BookmarkModel* bookmark_model =
      BookmarkModelFactory::GetForBrowserContext(profile);  >>> 
 const bool has_bookmarks = bookmark_model && bookmark_model->HasBookmarks();  <<< 
tab_groups::TabGroupSyncService* tab_group_service =
      tab_groups::TabGroupSyncServiceFactory::GetForProfile(profile);
 ... } ...  
```
### patch
```cpp
  const bool has_bookmarks = bookmark_model && bookmark_model->HasBookmarks() || true;

```

