### match
```cpp
...
 
 class JavaScriptTabModalDialogManagerDelegateDesktop
    : public javascript_dialogs::TabModalDialogManagerDelegate,
      public BrowserCollectionObserver,
      public TabStripModelObserver { ... 
~JavaScriptTabModalDialogManagerDelegateDesktop() override;
 // javascript_dialogs::TabModalDialogManagerDelegate 
 >>> 
base::WeakPtr<javascript_dialogs::TabModalDialogView> CreateNewDialog(
      content::WebContents* alerting_web_contents,
      const std::u16string& title,
      content::JavaScriptDialogType dialog_type,
      const std::u16string& message_text,
      const std::u16string& default_prompt_text,
      content::JavaScriptDialogManager::DialogClosedCallback dialog_callback,
      base::OnceClosure dialog_closed_callback) override;
 ... } ...  
```
### patch
```cpp
  base::WeakPtr<javascript_dialogs::TabModalDialogView> CreateNewDialog_ChromiumImpl(                                               
      content::WebContents* alerting_web_contents,
      const std::u16string& title, content::JavaScriptDialogType dialog_type,
      const std::u16string& message_text,
      const std::u16string& default_prompt_text,
      content::JavaScriptDialogManager::DialogClosedCallback dialog_callback,
      base::OnceClosure dialog_closed_callback);

```

