### match
```cpp
...
 
 # ifndef ... 
#include "content/public/browser/web_contents.h"

 #include "content/public/browser/web_contents_user_data.h"
 
 >>> 
namespace credential_management {
class ContentCredentialManager;
}
 ... 
```
### patch
```cpp
#include "components/autofill/content/browser/content_autofill_driver_factory.h"
#include "components/autofill/content/common/mojom/autofill_agent.mojom.h"
#include "components/autofill/core/browser/foundations/autofill_client.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace autofill { ...   >>> 
 : 
 public 
 AutofillClient 
 ,  <<< 
public
 ... } ...  
```
### patch
```cpp
    : public BraveContentAutofillClientUnused, public AutofillClient,

```
