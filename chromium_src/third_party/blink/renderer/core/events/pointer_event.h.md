### match
```
...
 # ifndef ... 
 namespace blink { ... 
 double screenX() const override { ... 
if (ShouldHaveIntegerCoordinates())
      return MouseEvent::screenX();  >>> 
 return screen_x_;  <<< ... } ...  } ...  
```
### patch
```
    return brave::FarbledPointerScreenCoordinate(
      view(), brave::FarbleKey::kPointerScreenX, client_x_, screen_x_);;

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 double screenY() const override { ... 
if (ShouldHaveIntegerCoordinates())
      return MouseEvent::screenY();  >>> 
 return screen_y_;  <<< ... } ...  } ...  
```
### patch
```
    return brave::FarbledPointerScreenCoordinate( 
      view(), brave::FarbleKey::kPointerScreenY, client_y_, screen_y_);;

```

