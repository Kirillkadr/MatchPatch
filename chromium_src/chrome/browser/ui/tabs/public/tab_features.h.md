### match
```cpp
...
 
 namespace tabs { ... 
  >>> 
 void Init(TabInterface& tab, Profile* profile);  <<< 
static ui::UserDataFactoryWithOwner<TabInterface>&
  GetUserDataFactoryForTesting();
 ... } ...
```
### patch
```cpp
virtual void Init(TabInterface& tab, Profile* profile);

```

