### match
```
...
 
 # ifndef ... 
void NotifyImportItemEnded(user_data_importer::ImportItem item);  >>> 
 void NotifyImportEnded();  <<< 
private
 ... 
```
### patch
```
  void virtual NotifyImportEnded();
  friend class BraveExternalProcessImporterHost;
  void set_parent_view(gfx::NativeView parent_view) {
    parent_view_ = parent_view;
  }                                                   
  gfx::NativeView parent_view_ = gfx::NativeView();

```

