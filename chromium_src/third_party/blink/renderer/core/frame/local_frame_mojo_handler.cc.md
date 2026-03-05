### match
```
...
 namespace 
 blink 
 { 
 >>> 
namespace {
...
}
...
```
### patch
```
void LocalFrameMojoHandler::GetImageAt(const gfx::Point& window_point,
                                       GetImageAtCallback callback) {
  gfx::Point viewport_position =
      frame_->GetWidgetForLocalRoot()->DIPsToRoundedBlinkSpace(window_point);
  std::move(callback).Run(frame_->GetImageAtViewportPoint(viewport_position));
}

```

