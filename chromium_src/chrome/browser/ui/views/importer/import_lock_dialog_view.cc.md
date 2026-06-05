### match
```cpp
...
 ImportLockDialogView::~ImportLockDialogView() = default; 
 >>> 
 ... 
```
### patch
```cpp
namespace importer {
void ShowImportLockDialog(gfx::NativeView parent_view,
                          gfx::NativeWindow parent,
                          base::OnceCallback<void(bool)> callback,
                          int importer_lock_title_id,
                          int importer_lock_text_id) {
  ImportLockDialogView::Show(parent_view, parent, std::move(callback),
                             importer_lock_title_id, importer_lock_text_id);
}

}  // namespace importer

// static
void ImportLockDialogView::Show(gfx::NativeView parent_view,
                                gfx::NativeWindow parent,
                                base::OnceCallback<void(bool)> callback,
                                int importer_lock_title_id,
                                int importer_lock_text_id) {
  views::DialogDelegate::CreateDialogWidget(
      new ImportLockDialogView(std::move(callback), importer_lock_title_id,
                               importer_lock_text_id),
      parent, parent_view)
      ->Show();
  base::RecordAction(UserMetricsAction("ImportLockDialogView_Shown"));
}

ui::mojom::ModalType ImportLockDialogView::GetModalType() const {
  return ui::mojom::ModalType::kChild;
}

```

