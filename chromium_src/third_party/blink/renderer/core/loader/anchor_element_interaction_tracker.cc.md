### match
```
...
 namespace blink { ... 
 void AnchorElementInteractionTracker::OnPointerEvent(
    EventTarget& target,
    const PointerEvent& pointer_event) { ... 
 if (event_type == event_type_names::kPointerdown) { ... 
last_pointer_down_locations_[1] = last_pointer_down_locations_[0];  >>> 
 last_pointer_down_locations_[0] = pointer_event.screenY();  <<< ... 
if (auto* viewport_position_tracker =
            AnchorElementViewportPositionTracker::MaybeGetOrCreateFor(
                *GetDocument())) {
      viewport_position_tracker->RecordPointerDown(pointer_event);
    }
 ... } ...  } ...  } ...  
```
### patch
```
    last_pointer_down_locations_[0] = pointer_event.screenY_ChromiumImpl();

```

### match
```
...
 namespace blink { ... 
 void AnchorElementInteractionTracker::OnClickEvent(
    HTMLAnchorElementBase& anchor,
    const MouseEvent& click_event) { ... 
const char* orientation_pattern =
      screen->width() <= screen_height ? ".Portrait" : ".Landscape";  >>> 
 double click_y = click_event.screenY();  <<< ... 
int normalized_click_y = base::ClampRound(100.0f * (click_y / screen_height));
 ... } ...  } ...  
```
### patch
```
  double click_y = click_event.screenY_ChromiumImpl();

```

