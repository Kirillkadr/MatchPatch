### match
```cpp
...
#include <unordered_set>

 #include <utility>
 
 >>> 
#include "base/files/file_path.h"

 ... 
```
### patch
```cpp
#include <algorithm>
#include "components/bookmarks/browser/bookmark_node.h"

```

### match
```cpp
...
 
 namespace bookmarks { ... 
 
 std::vector<const BookmarkNode*> GetMostRecentlyModifiedUserFolders(
    BookmarkModel* model) { ... 
auto more_recently_modified = [account_permanent_nodes_possibly_null,
                                 default_node](const BookmarkNode* n1,
                                               const BookmarkNode* n2) {
    base::Time t1 =
        std::ranges::contains(account_permanent_nodes_possibly_null, n1)
            ? std::max(n1->date_folder_modified(), n1->date_added())
            : n1->date_folder_modified();

    base::Time t2 =
        std::ranges::contains(account_permanent_nodes_possibly_null, n2)
            ? std::max(n2->date_folder_modified(), n2->date_added())
            : n2->date_folder_modified();

    // If no node has been modified more recently, choose a default folder.
    return t1 == t2 ? (n1 == default_node || n2 != default_node) : (t1 > t2);
  };  >>> 
 std::ranges::stable_sort(nodes, more_recently_modified);  <<< 
return nodes;
 ... } ...  } ...  
```
### patch
```cpp
  std::ranges::stable_sort(nodes, [](const bookmarks::BookmarkNode* n1,
                        const bookmarks::BookmarkNode* n2) {
    return n1->date_folder_modified() > n2->date_folder_modified();
  });                                                               
  more_recently_modified;;

```

