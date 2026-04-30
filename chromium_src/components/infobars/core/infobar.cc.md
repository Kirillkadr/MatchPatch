### match
```cpp
...
 
 namespace infobars { ... 
 
 base::WeakPtr<InfoBar> InfoBar::AsWeakPtr() { ... 
return weak_factory_.GetWeakPtr();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void InfoBar::BraveSetTargetHeight(int height) {
  target_height_ = height;
  height_ = animation_.CurrentValueBetween(0, target_height_);
}

```

