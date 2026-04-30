### match
```cpp
...
 
 namespace javascript_dialogs { ... 
 void TabModalDialogManager::OnVisibilityChanged ( ... 
 content::Visibility visibility 
 ) 
 { 
 >>> 
if (visibility == content::Visibility::HIDDEN) {
    HandleTabSwitchAway(DismissalCause::kTabHidden);
  } else if (pending_dialog_) {
    // Another dialog has started showing between when the pending dialog was
    // created and now. We cannot show the pending dialog over the currently
    // showing dialog, so we must close the pending dialog.
    if (!delegate_->CanShowModalUI()) {
      CloseDialog(DismissalCause::kSuppressedByOtherDialog, false,
                  std::u16string());
      return;
    }

    dialog_ = std::move(pending_dialog_).Run();
    pending_dialog_.Reset();
    delegate_->SetTabNeedsAttention(false);
  }
 ... } ...  } ...
```
### patch
```cpp
if (visibility != content::Visibility::HIDDEN &&           
      !delegate_->IsWebContentsForemost()) {
    visibility = content::Visibility::HIDDEN;
  }

```

### match
```cpp
...
  WEB_CONTENTS_USER_DATA_KEY_IMPL(TabModalDialogManager); 
 >>> 
 ...
```
### patch
```cpp
void TabModalDialogManager::OnTabActiveStateChanged() {
  OnVisibilityChanged(web_contents()->GetVisibility());
}

```

