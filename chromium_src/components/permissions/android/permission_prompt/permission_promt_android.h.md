### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
 
 class PermissionPromptAndroid : public PermissionPrompt { ... 
// We show one permission at a time except for grouped mic+camera, for which
 // we still have a single icon and message text. 
 >>> 
size_t PermissionCount() const;
 ... } ...  } ...  
```
### patch
```cpp
  size_t NotUsed() {
    return 0;
  }
  /* We can't override delegate to make it public, because at              */
  /* permission_prompt_android.h delegate is used both                     */
  /* as the argument name and the method name */
  Delegate* delegate_public() const {
    return delegate_;
  }
  /* Public setter for upstream's private permission_dialog_delegate_      */
  void set_permission_dialog_delegate(
      std::unique_ptr<PermissionDialogDelegate> permission_dialog_delegate) {
    permission_dialog_delegate_ = std::move(permission_dialog_delegate);
  }

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
 
 class PermissionPromptAndroid : public PermissionPrompt { ... 
std::unique_ptr<PermissionDialogDelegate> permission_dialog_delegate_;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
class PermissionPromptAndroid : public PermissionPromptAndroid_ChromiumImpl {
 public:
  using PermissionPromptAndroid_ChromiumImpl::
      PermissionPromptAndroid_ChromiumImpl;
  PermissionPromptAndroid(const PermissionPromptAndroid&) = delete;
  PermissionPromptAndroid& operator=(const PermissionPromptAndroid&) = delete;

  ~PermissionPromptAndroid() override = default;

  int GetIconId() const override;
  bool ShouldUseRequestingOriginFavicon() const override;

  void CreatePermissionDialogDelegate() {
    // This method does the same as upstream's
    // PermissionPromptAndroid::CreatePermissionDialogDelegate:
    // permission_dialog_delegate_ =
    //     PermissionDialogDelegate::Create(web_contents_, this);
    std::unique_ptr<PermissionDialogDelegate> permission_dialog_delegate =
        PermissionDialogDelegate::Create(web_contents(), this);
    set_permission_dialog_delegate(std::move(permission_dialog_delegate));
  }
};

```

