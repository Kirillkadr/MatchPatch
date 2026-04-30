### match
```cpp
...
 
 # ifndef ... 
#include <utility>

 #include <vector>
 
 >>> 
#include "base/containers/flat_map.h"

 ...
```
### patch
```cpp
#include "content/public/browser/render_frame_host.h"
#include "third_party/blink/public/mojom/frame/frame.mojom.h"

```

### match
```cpp
... 
void ActivateFindInPageResultForAccessibility(int request_id) override;
 void InsertVisualStateCallback(VisualStateCallback callback) override; 
 >>> 
void CopyImageAt(int x, int y) override;
 ...
```
### patch
```cpp
cpp
  void GetImageAt(int x, int y, base::OnceCallback<void(const SkBitmap&)> callback) override;
```

### match
```cpp
... 
 (mojo::PendingReceiver<network::mojom::TrustTokenQueryAnswerer> receiver 
 ) 
 ; 
 >>> 
 ...
```
### patch
```cpp
  void BindTrustTokenQueryAnswerer_ChromiumImpl(
      mojo::PendingReceiver<network::mojom::TrustTokenQueryAnswerer> receiver);

```

### match
```cpp
...
 std::optional<base::UnguessableToken> embedding_token_; 
 >>> ...
```
### patch
```cpp
  std::optional<base::UnguessableToken> ephemeral_storage_token_;
  bool ephemeral_storage_token_set_ = false;
  void SetEphemeralStorageToken(const url::Origin& top_frame_origin);
  std::optional<base::UnguessableToken> GetEphemeralStorageToken() const;


```

### match
```cpp
...
    >>> 
		  void GetImageAt(int x, int y, base::OnceCallback<void(const SkBitmap&)> callback) override; 
 void CopyImageAt(int x, int y) override;  <<< 
 ...
```
### patch
```cpp
cpp
  void GetImageAt(int x, int y, base::OnceCallback<void(const SkBitmap&)> callback) override;
  void CopyImageAt(int x, int y) override;
```

### match
```cpp
...
>>>
 cpp 
 cpp  <<<  ...
```
### patch
```cpp

```

