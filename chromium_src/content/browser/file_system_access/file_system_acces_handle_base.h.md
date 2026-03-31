### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 class CONTENT_EXPORT FileSystemAccessHandleBase { ... 
// Implementation for the Move method in the
 // blink::mojom::FileSystemAccessFileHandle and DirectoryHandle interfaces. 
 >>> 
void DoMove(mojo::PendingRemote<blink::mojom::FileSystemAccessTransferToken>
                  destination_directory,
              const std::string& new_entry_name,
              bool has_transient_user_activation,
              base::OnceCallback<void(blink::mojom::FileSystemAccessErrorPtr)>
                  callback);
 ... } ...  } ...  
```
### patch
```cpp
  void DoMove_ChromiumImpl(mojo::PendingRemote<blink::mojom::FileSystemAccessTransferToken>
                  destination_directory,
              const std::string& new_entry_name,
              bool has_transient_user_activation,
              base::OnceCallback<void(blink::mojom::FileSystemAccessErrorPtr)>
                  callback); \

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 class CONTENT_EXPORT FileSystemAccessHandleBase { ... 
// Implementation for the Rename method in the
 // blink::mojom::FileSystemAccessFileHandle and DirectoryHandle interfaces. 
 >>> 
void DoRename(const std::string& new_entry_name,
                bool has_transient_user_activation,
                base::OnceCallback<void(blink::mojom::FileSystemAccessErrorPtr)>
                    callback);
 ... } ...  } ...  
```
### patch
```cpp
  void DoRename_ChromiumImpl(const std::string& new_entry_name,
                bool has_transient_user_activation,
                base::OnceCallback<void(blink::mojom::FileSystemAccessErrorPtr)>
                    callback); \

```

