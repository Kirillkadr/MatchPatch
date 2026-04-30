### match
```cpp
...
 
 class OmniboxEditModel { ... 
void StartAutocomplete(bool prevent_inline_autocomplete);
 // Determines whether the user can "paste and go", given the specified text. 
 >>> 
bool CanPasteAndGo(const std::u16string& text) const;
 ... } ...  
```
### patch
```cpp
  bool CanPasteAndGo_Chromium(const std::u16string& text) const;

```

### match
```cpp
...
 
 class OmniboxEditModel { ... 
bool CanPasteAndGo(const std::u16string& text) const;
 // Navigates to the destination last supplied to CanPasteAndGo. 
 >>> 
void PasteAndGo(
      const std::u16string& text,
      base::TimeTicks match_selection_timestamp = base::TimeTicks());
 ... } ...  
```
### patch
```cpp
  void  PasteAndGo_Chromium(const std::u16string& text,
                      base::TimeTicks match_selection_timestamp);

```

