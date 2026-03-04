### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
 
 class ExtensionService : public ExtensionServiceInterface,
                         public content::RenderProcessHostCreationObserver,
                         public content::RenderProcessHostObserver,
                         public Blocklist::Observer,
                         public CWSInfoService::Observer,
                         public ExtensionManagement::Observer,
                         public policy::ExtensionInstallPolicyService::Observer,
                         public UpgradeObserver,
                         public ExtensionHostRegistry::Observer,
                         public ProfileManagerObserver { ... 
friend class SafeBrowsingVerdictHandlerUnitTest;
 friend class BlocklistStatesInteractionUnitTest; 
 >>> 
 ... } ...  } ...  
```
### patch
```
  friend class BraveExtensionService;

```

