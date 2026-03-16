### match
```
...
 # ifndef ... 
 #define CHROME_BROWSER_BROWSING_DATA_CHROME_BROWSING_DATA_REMOVER_DELEGATE_FACTORY_H_
 
 >>> 
#include "chrome/browser/profiles/profile_keyed_service_factory.h"

 ... 
```
### patch
```
#include "brave/browser/browsing_data/brave_browsing_data_remover_delegate.h"

```

### match
```
...
 # ifndef ... 
namespace base {
template <typename T>
class NoDestructor;
}  >>> 
 class ChromeBrowsingDataRemoverDelegate 
 ;  <<< ... 
class Profile
 ... 
```
### patch
```
class BraveBrowsingDataRemoverDelegate;

```

### match
```
...
 # ifndef ... 
// Returns the ChromeBrowsingDataRemoverDelegate associated with |profile|.  >>> 
 static ChromeBrowsingDataRemoverDelegate* GetForProfile(Profile* profile);  <<< ... 
ChromeBrowsingDataRemoverDelegateFactory(
      const ChromeBrowsingDataRemoverDelegateFactory&) = delete;
 ... 
```
### patch
```
  static BraveBrowsingDataRemoverDelegate* GetForProfile(Profile* profile);

```

