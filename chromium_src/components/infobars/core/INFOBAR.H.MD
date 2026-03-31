### match
```cpp
...
 
 # ifndef ... 
 
 namespace infobars { ... 
 
 class InfoBar : public gfx::AnimationDelegate { ... 
void RemoveSelf();
 // Changes the target height of the infobar. 
 >>> 
void SetTargetHeight(int height);
 ... } ...  } ...  
```
### patch
```cpp
  void BraveSetTargetHeight(int height); 

```

