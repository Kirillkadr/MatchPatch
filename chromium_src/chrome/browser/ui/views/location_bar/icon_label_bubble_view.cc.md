### match
```cpp
...
 
 views::ProposedLayout IconLabelBubbleView::CalculateProposedLayout(
    const views::SizeBounds& size_bounds) const { ... 
>>> 
 if 
 (ShouldShowLabel() && label()->GetElideBehavior() != gfx::NO_ELIDE) 
 { 
<<< 
...} ...  } ...  
```
### patch
```cpp
    if ((ShouldShowLabel() && label()->GetElideBehavior() != gfx::NO_ELIDE) || ShouldAlwaysShowLabel()) {

```

### match
```cpp
...
>>>
 const 
 bool 
 should_use_label_bounds 
 = 
<<< 
...
```
### patch
```cpp
  bool should_use_label_bounds =

```

### match
```cpp
...
 
 views::ProposedLayout IconLabelBubbleView::CalculateProposedLayout(
    const views::SizeBounds& size_bounds) const { ... 
 ShouldShowLabel() && (can_label_expand || can_expand_label_for_animation) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
      should_use_label_bounds = should_use_label_bounds || ShouldAlwaysShowLabel();

```

### match
```cpp
...
 
 SkPath IconLabelBubbleView::GetHighlightPath() const { ... 
>>> 
 const SkRect rect = RectToSkRect(highlight_bounds); 
 gfx::RoundedCornersF radii = GetCornerRadii(); 
 const SkVector sk_radii[4] = {{radii.upper_left(), radii.upper_left()},
                                {radii.upper_right(), radii.upper_right()},
                                {radii.lower_right(), radii.lower_right()},
                                {radii.lower_left(), radii.lower_left()}}; 
 return SkPath::RRect(SkRRect::MakeRectRadii(rect, sk_radii)); 
<<< 
...} ...  
```
### patch
```cpp
  const int layout_radius =
      GetLayoutConstant(LayoutConstant::kLocationBarChildCornerRadius);
  return SkPath::RRect(gfx::RectToSkRect(highlight_bounds), layout_radius,
                       layout_radius);

```

