### match
```cpp
...
// base for the classes that handle the location icon (including the EV bubble),
 // tab-to-search UI, and content settings. 
 >>> 
 ... 
```
### patch
```cpp
class BraveLocationBarView;

```

### match
```cpp
...
 
 class IconLabelBubbleView : public views::InkDropObserver,
                            public views::LabelButton { ... 
 // Sets the label text and background colors. 
 >>> 
 ... } ...  
```
### patch
```cpp
  friend class BraveLocationBarView; 

```

