### match
```cpp
...
 
 namespace security_interstitials { ... 
 
 class BaseSafeBrowsingErrorUI { ... 
>>> 
 bool 
 CanShowEnhancedProtectionMessage() 
 { 
<<< 
return !is_off_the_record() && is_enhanced_protection_message_enabled() &&
           !is_safe_browsing_managed() && !is_enhanced_protection_enabled();
 ... } ...  } ...  } ...  
```
### patch
```cpp
  bool CanShowEnhancedProtectionMessage() { return false; } 
  bool CanShowEnhancedProtectionMessage_ChromiumImpl() {

```

