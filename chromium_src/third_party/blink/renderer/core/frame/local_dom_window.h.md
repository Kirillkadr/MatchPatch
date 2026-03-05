### match
```
...
 # ifndef ... 
 namespace blink { ... 
Navigator* clientInformation() { return navigator(); }
 bool offscreenBuffering() const; 
 >>> 
int outerHeight() const;
 ... } ...  
```
### patch
```
  int outerHeight_ChromiumImpl() const;

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
int outerHeight_ChromiumImpl() const;
 int outerHeight() const; 
 >>> 
int outerWidth() const;
 ... } ...  
```
### patch
```
  int outerWidth_ChromiumImpl() const;

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
int screenX() const;
 int screenY() const; 
 >>> 
int screenLeft() const { return screenX(); }
 ... } ...  
```
### patch
```
  int screenX_ChromiumImpl() const;

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
int screenX_ChromiumImpl() const;
 int screenLeft() const { return screenX(); } 
 >>> 
int screenTop() const { return screenY(); }
 ... } ...  
```
### patch
```
  int screenY_ChromiumImpl() const;

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
void scrollToForTesting(double x, double y) const;
 void moveBy(int x, int y) const; 
 >>> 
void moveTo(int x, int y) const;
 ... } ...  
```
### patch
```
  void moveTo_ChromiumImpl(int x, int y) const;

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
void moveTo(int x, int y) const;
 void resizeBy(int x, int y, ExceptionState&) const; 
 >>> 
void resizeTo(int width, int height, ExceptionState&) const;
 ... } ...  
```
### patch
```
  void resizeTo_ChromiumImpl(int width, int height,
                        ExceptionState& exception_state) const;

```

### match
```
...
 # ifndef ... 
 inline String LocalDOMWindow::defaultStatus() const { ... 
return default_status_;
 } 
 >>> 
 ... 
```
### patch
```
CORE_EXPORT const SecurityOrigin* GetEphemeralStorageOrigin(
    LocalDOMWindow* window);

```

