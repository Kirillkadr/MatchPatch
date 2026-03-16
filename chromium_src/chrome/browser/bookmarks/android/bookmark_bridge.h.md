### match
```
...
 # ifndef ... 
#include "base/strings/utf_string_conversions.h"

 #include "base/supports_user_data.h"
 
 >>> 
#include "chrome/browser/partnerbookmarks/partner_bookmarks_shim.h"

 ... 
```
### patch
```
#include "base/threading/sequence_bound.h"

```

### match
```
...
 # ifndef ... 
#include "components/reading_list/core/reading_list_model_observer.h"

 #include "components/signin/public/identity_manager/identity_manager.h"
 
 >>> 
#include "url/android/gurl_android.h"

 ... 
```
### patch
```
#include "components/user_data_importer/utility/bookmark_parser.h"

```

### match
```
...
 # ifndef ... 
#include "components/user_data_importer/utility/bookmark_parser.h"

 #include "url/android/gurl_android.h"
 
 >>> 
class BookmarkBridgeTest
 ... 
```
### patch
```
namespace user_data_importer {
class ContentBookmarkParser;
}


```

### match
```
...
 # ifndef ... 
 class BookmarkBridge : public ProfileObserver,
                       public bookmarks::BaseBookmarkModelObserver,
                       public PartnerBookmarksShim::Observer,
                       public reading_list::ReadingListManager::Observer,
                       public ReadingListModelObserver,
                       public signin::IdentityManager::Observer,
                       public base::SupportsUserData::Data { ... 

      JNIEnv* env,
      const base::android::JavaRef<jobject>& j_parent_id_obj,
      const std::string& title,
      
 const GURL& url 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```
  void ImportBookmarks(JNIEnv* env, const base::android::JavaRef<jobject>& obj,
                  const base::android::JavaRef<jobject>& java_window,
                  const base::android::JavaRef<jstring>& import_file_path);
  void OnParseFinished(
      user_data_importer::BookmarkParser::BookmarkParsingResult result);
  base::SequenceBound<user_data_importer::ContentBookmarkParser>
      bookmark_parser_;
  void ExportBookmarks(
      JNIEnv* env, const base::android::JavaRef<jobject>& obj,
      const base::android::JavaRef<jobject>& java_window,
      const base::android::JavaRef<jstring>& export_file_path);             

```

