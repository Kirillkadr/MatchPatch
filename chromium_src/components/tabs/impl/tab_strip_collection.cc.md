### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
 ...
```
### patch
```cpp
#include "components/tabs/public/tab_strip_collection.h"

```

### match
```cpp
...
 
 namespace tabs { ... 
>>> 
 std::unique_ptr<TabInterface> 
 TabStripCollection::RemoveTabAtIndexRecursive 
 ( 
<<< 
...) ...  } ...
```
### patch
```cpp
std::unique_ptr<TabInterface> TabStripCollection::RemoveTabAtIndexRecursive_Chromium(

```

### match
```cpp
...
 
 namespace tabs { ... 
 >>>  } ...
```
### patch
```cpp
std::unique_ptr<TabInterface> TabStripCollection::RemoveTabAtIndexRecursive(
    size_t index) {
#if !BUILDFLAG(IS_ANDROID)
  TabInterface* tab_to_be_removed = GetTabAtIndexRecursive(index);
  TabCollection* parent_collection =
      tab_to_be_removed->GetParentCollection(GetPassKey());
  CHECK(parent_collection);
  if (parent_collection->type() == TabCollection::Type::TREE_NODE) {
    // When it's tree node, bypass upstream's implementation so that we can
    // avoid crash from RemoveTabCollectionImpl(parent_collection). Calling this
    // will destroy the storage and the tab in the storage, but we should return
    // the tab for further processing.
    // TODO(https://github.com/brave/brave-browser/issues/49789) This should be
    // revisited once tab removal cases are fully handled for tree tabs.
    auto tab = RemoveTabImpl(tab_to_be_removed);

    if (auto* grand_parent = parent_collection->GetParentCollection();
        grand_parent && grand_parent->type() == TabCollection::Type::GROUP &&
        grand_parent->TabCountRecursive() == 0) {
      // If the grand parent is a group, we need to close the tab group when the
      // removed tab was the only descendant tab of the group.
      RemoveTabCollectionImpl(grand_parent);
    }

    return tab;
  }
#endif  // !BUILDFLAG(IS_ANDROID)

  return RemoveTabAtIndexRecursive_Chromium(index);
}

void TabStripCollection::AddTabRecursive(
    std::unique_ptr<TabInterface> tab,
    size_t index,
    std::optional<tab_groups::TabGroupId> new_group_id,
    bool new_pinned_state,
    TabInterface* opener) {
  // Default implementation just calls the base class method without opener.
  // This method will be overriden in BraveTabStripCollection and use opener
  // for tree tab mod
  AddTabRecursive(std::move(tab), index, new_group_id, new_pinned_state);
}

```

