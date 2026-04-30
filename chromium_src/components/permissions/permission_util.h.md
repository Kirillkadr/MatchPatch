### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ...   >>> 
 class 
 PermissionUtil 
 {  <<< 
public
 ... } ...  } ...
```
### patch
```cpp
cpp
class PermissionUtil_ChromiumImpl {
```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
 
 class PermissionUtil_ChromiumImpl { ...   >>> 
 PermissionUtil() = delete; 
 PermissionUtil(const PermissionUtil&) = delete; 
 PermissionUtil& operator=(const PermissionUtil&) = delete;  <<< 
// Returns the permission string for the given permission.
 ... } ...  } ...
```
### patch
```cpp
  PermissionUtil_ChromiumImpl() = delete;
  PermissionUtil_ChromiumImpl(const PermissionUtil_ChromiumImpl&) = delete;
  PermissionUtil_ChromiumImpl& operator=(const PermissionUtil_ChromiumImpl&) = delete;

```

### match
```cpp
...
 >>> 
#endif  // COMPONENTS_PERMISSIONS_PERMISSION_UTIL_H_
 ...
```
### patch
```cpp
namespace permissions {
class PermissionUtil : public PermissionUtil_ChromiumImpl {
 public:
  static std::string GetPermissionString(ContentSettingsType);
  static bool GetPermissionType(ContentSettingsType type,
                                blink::PermissionType* out);
  static bool IsPermission(ContentSettingsType type);

  static blink::PermissionType ContentSettingsTypeToPermissionType(
      ContentSettingsType permission);

  static GURL GetCanonicalOrigin(ContentSettingsType permission,
                                 const GURL& requesting_origin,
                                 const GURL& embedding_origin);
};

}  // namespace permissions

```

### match
```cpp
...
>>>
 cpp 
 class 
 PermissionUtil_ChromiumImpl 
 { 
 public 
 :  <<< 
PermissionUtil_ChromiumImpl() = delete;
 ... } ...  
```
### patch
```cpp
class PermissionUtil_ChromiumImpl {
 public:

```

