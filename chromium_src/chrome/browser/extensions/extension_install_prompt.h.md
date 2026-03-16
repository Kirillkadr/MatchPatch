### match
```
...
 
 # ifndef ... 
 
 class ExtensionInstallPrompt : public extensions::ExtensionInstallPromptClient { ... 
 
 class Prompt { ... 
PromptType type() const { return type_; }
 // Getters for UI element labels. 
 >>> 
std::u16string GetDialogTitle() const;
 ... } ...  } ...  
```
### patch
```
    std::u16string GetDialogTitle_ChromiumImpl() const; 

```

