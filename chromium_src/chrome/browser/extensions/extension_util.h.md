### match
```
...
>>>
 std::unique_ptr<const PermissionSet> 
 GetInstallPromptPermissionSetForExtension 
 (  <<< 
const Extension* extension
 ... ) ...  
```
### patch
```
std::unique_ptr<const PermissionSet> GetInstallPromptPermissionSetForExtension_ChromiumImpl(

```

### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
 
 namespace util { ... 
const base::CommandLine& command_line,
                           
 content::BrowserContext* context 
 ) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```
std::unique_ptr<const PermissionSet> GetInstallPromptPermissionSetForExtension(
    const Extension* extension,
    Profile* profile);


```

