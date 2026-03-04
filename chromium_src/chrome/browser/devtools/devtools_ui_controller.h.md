### match
```
...
 
 # ifndef ... 
 
 class DevtoolsUIController { ... 
explicit DevtoolsUIController(
      std::vector<ContentsContainerView*> contents_container_views);
 ~DevtoolsUIController(); 
 >>> 
void TearDown();
 ... } ...  
```
### patch
```
  void MakeSureControllerExists(ContentsContainerView* view); 

```

