### match
```cpp
...
// found in the LICENSE file.
 #include "content/browser/file_system_access/file_system_access_handle_base.h"
 
 >>> 
#include <memory>

 ... 
```
### patch
```cpp
#include "content/browser/file_system_access/file_system_access_directory_handle_impl.h"

```

### match
```cpp
...
 
 namespace content { ...   >>> 
 void 
 FileSystemAccessHandleBase::DoMove 
 (  <<< 
mojo::PendingRemote<blink::mojom::FileSystemAccessTransferToken>
        destination_directory
 ... ) ...  } ...  
```
### patch
```cpp
void FileSystemAccessHandleBase::DoMove_ChromiumImpl(

```

### match
```cpp
...
 
 namespace content { ...   >>> 
 void 
 FileSystemAccessHandleBase::DoRename 
 (  <<< 
const std::string& new_entry_name
 ... ) ...  } ...  
```
### patch
```cpp
void FileSystemAccessHandleBase::DoRename_ChromiumImpl(

```

### match
```cpp
...
 
 namespace content { ... 
 
 void FileSystemAccessHandleBase::DidResolveTokenToMove(
    const std::string& new_entry_name,
    bool has_transient_user_activation,
    base::OnceCallback<void(blink::mojom::FileSystemAccessErrorPtr)> callback,
    FileSystemAccessTransferTokenImpl* resolved_destination_directory) { ... 
 dir_handle->GetChildURL(new_entry_name, &dest_url) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
      if (dest_url.type() != storage::FileSystemType::kFileSystemTypeTemporary) {
    std::move(callback).Run(file_system_access_error::FromStatus(
        blink::mojom::FileSystemAccessStatus::kNotSupportedError));
    return;
  }

```

### match
```cpp
...
 
 namespace content { ... 
 
 FileSystemAccessHandleBase::PermissionStatus
FileSystemAccessHandleBase::GetPermissionStatusForMode(
    blink::mojom::FileSystemAccessPermissionMode mode) { ... 
switch (mode) {
    case blink::mojom::FileSystemAccessPermissionMode::kRead:
      return GetReadPermissionStatus();
    case blink::mojom::FileSystemAccessPermissionMode::kReadWrite:
      return GetReadWritePermissionStatus();
    case blink::mojom::FileSystemAccessPermissionMode::kWrite:
      return GetWritePermissionStatus();
  }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void FileSystemAccessHandleBase::DoMove(
    mojo::PendingRemote<blink::mojom::FileSystemAccessTransferToken>
        destination_directory,
    const std::string& new_entry_name,
    bool has_transient_user_activation,
    base::OnceCallback<void(blink::mojom::FileSystemAccessErrorPtr)> callback) {
  if (url().type() != storage::FileSystemType::kFileSystemTypeTemporary) {
    std::move(callback).Run(file_system_access_error::FromStatus(
        blink::mojom::FileSystemAccessStatus::kNotSupportedError));
    return;
  }

  DoMove_ChromiumImpl(std::move(destination_directory), new_entry_name,
                      has_transient_user_activation, std::move(callback));
}

void FileSystemAccessHandleBase::DoRename(
    const std::string& new_entry_name,
    bool has_transient_user_activation,
    base::OnceCallback<void(blink::mojom::FileSystemAccessErrorPtr)> callback) {
  if (url().type() != storage::FileSystemType::kFileSystemTypeTemporary) {
    std::move(callback).Run(file_system_access_error::FromStatus(
        blink::mojom::FileSystemAccessStatus::kNotSupportedError));
    return;
  }

  DoRename_ChromiumImpl(new_entry_name, has_transient_user_activation,
                        std::move(callback));
}

```

