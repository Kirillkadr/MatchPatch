### match
```cpp
...
 group_(group_factory.Create(this, group_id, visual_data)) 
 {} 
 >>> 
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_ANDROID)
TabGroupTabCollection::TabGroupTabCollection(
    TabGroup::Factory& group_factory,
    tab_groups::TabGroupId group_id,
    tab_groups::TabGroupVisualData visual_data)
    : TabCollection(TabCollection::Type::GROUP,
                    {TabCollection::Type::SPLIT, TabCollection::Type::TREE_NODE},
                    /*supports_tabs=*/true),
      group_(group_factory.Create(this, group_id, visual_data)) {}
#endif  // !BUILDFLAG(IS_ANDROID)

```

