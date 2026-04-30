### match
```cpp
...
 
 # ifndef ... 
 
 namespace gcm { ... 
 
 class GCMDriverDesktop : public GCMDriver,
                         protected InstanceIDHandler { ... 
base::WeakPtrFactory<GCMDriverDesktop> weak_ptr_factory_{this};
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
class BraveGCMDriverDesktop : public GCMDriverDesktop {
 public:
  using GCMDriverDesktop::GCMDriverDesktop;
  ~BraveGCMDriverDesktop() override;

  void SetEnabled(bool enabled) override;

 protected:
  // GCMDriver implementation:
  GCMClient::Result EnsureStarted(GCMClient::StartMode start_mode) override;

 private:
  bool enabled_{false};
  bool initialized_{false};
};

```

