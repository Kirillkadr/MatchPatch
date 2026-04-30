### match
```cpp
...
// found in the LICENSE file.
 #include "components/password_manager/core/browser/ui/weak_check_utility.h"
 
 >>> 
#include <functional>

 ... 
```
### patch
```cpp
#include "base/strings/utf_string_conversions.h"

```

### match
```cpp
...
 namespace 
 password_manager 
 { 
 >>> 
std::u16string_view SafeTruncateUTF16(std::u16string_view str,
                                      size_t max_length) {
  if (str.length() <= max_length) {
    return str;
  }

  base::i18n::BreakIterator iter(str,
                                 base::i18n::BreakIterator::BREAK_CHARACTER);
  if (!iter.Init()) {
    return str.substr(0, max_length);
  }

  size_t char_count = 0;
  while (iter.Advance() && char_count < max_length) {
    char_count++;
  }
  return str.substr(0, iter.prev());
}
 ... } ...  
```
### patch
```cpp
int GetPasswordStrength(const std::string& password) {
  if (password.empty()) {
    return 0;
  }
  // The score returned by PasswordWeakCheck() is an integer between 0 and 4
  // (https://github.com/dropbox/zxcvbn). 0 is weakest.
  return (PasswordWeakCheck(base::UTF8ToUTF16(password)) + 1) / 5.0 * 100;
}

```

