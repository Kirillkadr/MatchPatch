### match
```
...
 namespace blink { ... 
 bool ChromeClient::Print(LocalFrame* frame) { ... 
return true;
 } 
 >>> 
 ... } ...  
```
### patch
```
const display::ScreenInfos& ChromeClient::BraveGetScreenInfos(
    LocalFrame& frame) const {
  return this->GetScreenInfos(frame);
}

```

