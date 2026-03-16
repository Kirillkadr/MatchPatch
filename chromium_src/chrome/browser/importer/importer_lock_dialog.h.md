### match
```
...
 
 # ifndef ... 
 
 namespace importer { ... 
 int importer_lock_text_id = IDS_IMPORTER_LOCK_TEXT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```
void ShowImportLockDialog(gfx::NativeView parent_view,
                          gfx::NativeWindow parent,
                          base::OnceCallback<void(bool)> callback,
                          int importer_lock_title_id = IDS_IMPORTER_LOCK_TITLE,
                          int importer_lock_text_id = IDS_IMPORTER_LOCK_TEXT);


```

