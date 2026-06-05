### match
```cpp
...
 
 class ImportLockDialogView : public views::DialogDelegateView { ... 
 int importer_lock_text_id = IDS_IMPORTER_LOCK_TEXT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
  static void Show(gfx::NativeView parent_view, gfx::NativeWindow parent,
                   base::OnceCallback<void(bool)> callback,
                   int importer_lock_title_id = IDS_IMPORTER_LOCK_TITLE,
                   int importer_lock_text_id = IDS_IMPORTER_LOCK_TEXT);
  ui::mojom::ModalType GetModalType() const override;

```

