### match
```cpp
...
  >>> 
 int GetStandardWidth(const bool is_split) const;  <<< 
 ...
```
### patch
```cpp
int virtual GetStandardWidth(const bool is_split) const;

```

### match
```cpp
...
 >>> 
 int GetPinnedWidth(const bool is_split) const;  <<< 
 ...
```
### patch
```cpp
virtual int GetPinnedWidth(const bool is_split) const;

```

### match
```cpp
...
 >>> 
 int GetMinimumActiveWidth(const bool is_split) const;  <<< 
 ...
```
### patch
```cpp
int virtual GetMinimumActiveWidth(const bool is_split) const;

```

### match
```cpp
...
 >>> 
 int GetTabOverlap() const;  <<< 
 ...
```
### patch
```cpp
virtual int GetTabOverlap() const;

```

### match
```cpp
...
 >>> 
 gfx::Size GetSeparatorSize() const;  <<< 
 ...
```
### patch
```cpp
gfx::Size virtual GetSeparatorSize() const;

```

### match
```cpp
...
>>> 
 gfx::Insets GetSeparatorMargins() const;  <<< 
 ...
```
### patch
```cpp
gfx::Insets virtual GetSeparatorMargins() const;

```

### match
```cpp
...
 >>> 
 int GetSeparatorCornerRadius() const;  <<< 
 ...
```
### patch
```cpp
int virtual GetSeparatorCornerRadius() const;

```

### match
```cpp
...
 >>> 
 int GetDragHandleExtension(int height) const;  <<< 
 ...
```
### patch
```cpp
int virtual GetDragHandleExtension(int height) const;

```

### match
```cpp
...
 >>> 
 int GetTopCornerRadius() const;  <<< 
 ...
```
### patch
```cpp
int virtual GetTopCornerRadius() const;

```

### match
```cpp
...
 >>> 
 int GetBottomCornerRadius() const;  <<< 
std::tuple<float, float, float, SkColor> GetContrastRatioValues(
      bool frame_active,
      const ui::ColorProvider* color_provider) const;
 ...
```
### patch
```cpp
int virtual GetBottomCornerRadius() const;

```

### match
```cpp
...
 >>> 
 gfx::Insets GetContentsInsets() const;  <<< 
 ...
```
### patch
```cpp
gfx::Insets virtual GetContentsInsets() const;

```

