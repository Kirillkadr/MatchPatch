### match
```cpp
...
 
 # ifndef ... 
#include "ui/display/display_observer.h"
  >>> 
 class ChromeBrowserMainParts 
 ;  <<< 
class PrefRegistrySimple
 ... 
```
### patch
```cpp
class ChromeBrowserMainParts_ChromiumImpl;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace chrome { ...   >>> 
 void AddMetricsExtraParts(ChromeBrowserMainParts* main_parts);  <<<  ...} ...  
```
### patch
```cpp
void AddMetricsExtraParts(ChromeBrowserMainParts_ChromiumImpl* main_parts);

```

