### match
```
...
 
 void DevtoolsUIController::DevtoolsWebViewController::RestoreFocus() { ... 
if (devtools_focus_tracker_.get()) {
    devtools_focus_tracker_->FocusLastFocusedExternalView();
  }
 } 
 >>> 
 ... 
```
### patch
```

void DevtoolsUIController::MakeSureControllerExists(
    ContentsContainerView* view) {
  if (devtools_web_view_controllers_.find(view) ==
      devtools_web_view_controllers_.end()) {
    devtools_web_view_controllers_[view] =
        std::make_unique<DevtoolsWebViewController>(view);
  }
}

```

