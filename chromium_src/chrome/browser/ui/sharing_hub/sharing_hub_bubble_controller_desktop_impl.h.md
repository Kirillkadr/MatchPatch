### match
```cpp
...
 
 namespace sharing_hub { ... 
void ShowBubble(share::ShareAttempt attempt) override;
 SharingHubBubbleView* sharing_hub_bubble_view() const override; 
 >>> 
bool ShouldOfferOmniboxIcon() override;
 ... } ...  
```
### patch
```cpp
  bool  ShouldOfferOmniboxIcon_ChromiumImpl(); 

```

