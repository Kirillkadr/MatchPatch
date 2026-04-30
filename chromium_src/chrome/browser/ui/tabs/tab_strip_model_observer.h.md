### match
```cpp
...
#include <vector>

 #include "base/memory/raw_ptr.h"
 
 >>> 
#include "chrome/browser/tab_list/tab_removed_reason.h"

 ... 
```
### patch
```cpp
#include "base/memory/raw_ref.h"
#include "brave/components/tabs/public/tree_tab_node.h"
#include "brave/components/tabs/public/tree_tab_node_id.h"

```

### match
```cpp
...
 
 class TabStripModelObserver { ... 
virtual void OnTabChangedAt(tabs::TabInterface* tab,
                              int index,
                              TabChangeType change_type);
 // Invoked when the pinned state of a tab changes. 
 >>> 
virtual void OnTabPinnedStateChanged(tabs::TabInterface* tab, int index);
 ... } ...  
```
### patch
```cpp
  virtual void TabCustomTitleChanged(content::WebContents* contents,
                        const std::optional<std::string>& custom_title) {}

```

### match
```cpp
...
virtual void TabCustomTitleChanged(content::WebContents* contents,
	                        const std::optional<std::string>& custom_title) {}
 virtual void OnTabPinnedStateChanged(tabs::TabInterface* tab, int index); 
 >>> 
// Called when the tab at `index` is added to the group with id `new_group` or
 ... 
```
### patch
```cpp
  // Add TreeTabChange type to represent changes in the tree tab structure.
struct TreeTabChange {
  enum Type {
    kNodeCreated,
    kNodeWillBeDestroyed,
  };

  struct Delta {
    virtual ~Delta() = default;
  };

  struct CreatedChange : public Delta {
    explicit CreatedChange(const tabs::TreeTabNode& node);
    ~CreatedChange() override;

    raw_ref<const tabs::TreeTabNode> node;
  };

  struct WillBeDestroyedChange : public Delta {
    explicit WillBeDestroyedChange(const tabs::TreeTabNode& node);
    ~WillBeDestroyedChange() override;

    raw_ref<const tabs::TreeTabNode> node;
  };

  TreeTabChange(Type type,
                tree_tab::TreeTabNodeId id,
                std::unique_ptr<Delta> delta);
  TreeTabChange(tree_tab::TreeTabNodeId id,
                const CreatedChange& created_change);
  TreeTabChange(tree_tab::TreeTabNodeId id,
                const WillBeDestroyedChange& destroyed_change);
  TreeTabChange(const TreeTabChange& other) = delete;
  TreeTabChange& operator=(const TreeTabChange& other) = delete;
  ~TreeTabChange();

  const CreatedChange& GetCreatedChange() const;
  const WillBeDestroyedChange& GetWillBeDestroyedChange() const;

  Type type;
  tree_tab::TreeTabNodeId id;
  std::unique_ptr<Delta> delta;
};


```

### match
```cpp
...
// independent of the tabstrip model and do not affect any tab state.
 virtual void OnTabGroupChanged(const TabGroupChange& change); 
 >>> 
// Called when the "GroupFocused" state changes. This will happen before the
 ... 
```
### patch
```cpp
   virtual void OnTreeTabChanged(const TreeTabChange& change);

```

