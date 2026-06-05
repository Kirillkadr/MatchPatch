### match
```cpp
...
// model has changed.
>>> 
 void SetMatch(const AutocompleteMatch& match); 
<<< 
// Applies the current theme to the current text and widget colors.
 ... 
```
### patch
```cpp
  friend class BraveOmniboxResultView;
  virtual void SetMatch(const AutocompleteMatch& match);

```

### match
```cpp
...
// Invoked when this result view has been selected or unselected.
>>> 
 void OnSelectionStateChanged(); 
<<< 
// Whether this result view should be considered 'selected'. This returns
 ... 
```
### patch
```cpp
  virtual void OnSelectionStateChanged();

```

### match
```cpp
...
>>>
 gfx::Image GetIcon() const; 
<<< 
// Updates the highlight state of the row, as well as conditionally shows
 ... 
```
### patch
```cpp
  gfx::Image virtual GetIcon() const;

```

