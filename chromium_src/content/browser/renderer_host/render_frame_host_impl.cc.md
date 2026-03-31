### match
```cpp
...
// found in the LICENSE file.
 #include "content/browser/renderer_host/render_frame_host_impl.h"
 
 >>> 
#include <algorithm>

 ...
```
### patch
```cpp
#include "base/check.h"
#include "base/logging.h"

```

### match
```cpp
... 
prerender_state_callback_ = prerender_state_callback;

 >>> 
 ...
```
### patch
```cpp
void RenderFrameHostImpl::GetImageAt(
    int x,
    int y,
    base::OnceCallback<void(const SkBitmap&)> callback) {
  gfx::PointF point_in_view =
      GetView()->TransformRootPointToViewCoordSpace(gfx::PointF(x, y));
  GetAssociatedLocalFrame()->GetImageAt(
      gfx::Point(point_in_view.x(), point_in_view.y()), std::move(callback));
}
void RenderFrameHostImpl::SetEphemeralStorageToken(
    const url::Origin& top_frame_origin) {
  if (!is_main_frame()) {
    return;
  }

  ephemeral_storage_token_ =
      GetContentClient()->browser()->GetEphemeralStorageToken(this,
                                                              top_frame_origin);
  ephemeral_storage_token_set_ = true;

  DVLOG(2) << __func__ << " " << top_frame_origin << " "
           << (ephemeral_storage_token_ ? ephemeral_storage_token_->ToString()
                                        : std::string());
}

std::optional<base::UnguessableToken>
RenderFrameHostImpl::GetEphemeralStorageToken() const {
  const RenderFrameHostImpl* main_rfh = this;
  while (main_rfh->parent_) {
    main_rfh = main_rfh->parent_;
  }

  CHECK(main_rfh->ephemeral_storage_token_set_)
      << "RenderFrameHostImpl::SetEphemeralStorageToken wasn't called for the "
         "main frame";
  return main_rfh->ephemeral_storage_token_;
}

void RenderFrameHostImpl::BindTrustTokenQueryAnswerer(
    mojo::PendingReceiver<network::mojom::TrustTokenQueryAnswerer> receiver) {
  mojo::ReportBadMessage(
      "Attempted to get a TrustTokenQueryAnswerer with Private State Tokens "
      "disabled.");
  return;
}

```
