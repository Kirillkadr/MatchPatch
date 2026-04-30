### match
```cpp
...
#include "base/check_op.h"

 #include "base/trace_event/trace_event.h"
 
 >>> 
#include "chrome/browser/ui/tabs/tab_strip_model.h"

 ... 
```
### patch
```cpp
#include "brave/components/tabs/public/tree_tab_node.h"

```

### match
```cpp
...
 
 void TabStripModelObserver::ModelDestroyed(TabStripModelObserver::ModelPasskey,
                                           TabStripModel* model) { ... 
OnTabStripModelDestroyed(model);
 } 
 >>> 
 ... 
```
### patch
```cpp

TreeTabChange::CreatedChange::CreatedChange(const tabs::TreeTabNode& node)
    : node(node) {}

TreeTabChange::CreatedChange::~CreatedChange() = default;

TreeTabChange::WillBeDestroyedChange::WillBeDestroyedChange(
    const tabs::TreeTabNode& node)
    : node(node) {}

TreeTabChange::WillBeDestroyedChange::~WillBeDestroyedChange() = default;

TreeTabChange::TreeTabChange(Type type,
                             tree_tab::TreeTabNodeId id,
                             std::unique_ptr<Delta> delta)
    : type(type), id(id), delta(std::move(delta)) {}

TreeTabChange::TreeTabChange(tree_tab::TreeTabNodeId id,
                             const CreatedChange& created_change)
    : TreeTabChange(Type::kNodeCreated,
                    id,
                    std::make_unique<CreatedChange>(created_change)) {}

TreeTabChange::TreeTabChange(tree_tab::TreeTabNodeId id,
                             const WillBeDestroyedChange& destroyed_change)
    : TreeTabChange(Type::kNodeWillBeDestroyed,
                    id,
                    std::make_unique<WillBeDestroyedChange>(destroyed_change)) {
}

TreeTabChange::~TreeTabChange() = default;

const TreeTabChange::CreatedChange& TreeTabChange::GetCreatedChange() const {
  CHECK_EQ(type, Type::kNodeCreated);
  return *static_cast<CreatedChange*>(delta.get());
}

const TreeTabChange::WillBeDestroyedChange&
TreeTabChange::GetWillBeDestroyedChange() const {
  CHECK_EQ(type, Type::kNodeWillBeDestroyed);
  return *static_cast<WillBeDestroyedChange*>(delta.get());
}

void TabStripModelObserver::OnTreeTabChanged(const TreeTabChange& change) {}
```

