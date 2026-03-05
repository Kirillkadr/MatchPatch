### match
```
...
 namespace blink { ... 
 const display::ScreenInfo& Screen::GetScreenInfo() const { ... 
LocalFrame* frame = DomWindow()->GetFrame();  >>> 
 const auto& screen_infos = frame->GetChromeClient().GetScreenInfos(*frame);  <<< ... 
for (const auto& screen : screen_infos.screen_infos) {
    if (screen.display_id == display_id_)
      return screen;
  }
 ... } ...  } ...  
```
### patch
```
  const auto& screen_infos = frame->GetChromeClient().BraveGetScreenInfos(*frame);

```

