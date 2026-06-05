### match
```cpp
...
>>>
is_ask_starter_pack()     
<<< 
 ... 
```
### patch
```cpp
  is_ask_starter_pack() const {                            
    if (starter_pack_id() ==                               
        template_url_starter_pack_data::kAskBraveSearch) { 
      return true;                                         
    }                                                      
    return is_ask_starter_pack_chromium();                 
  }                                                        
  bool is_ask_starter_pack_chromium()

```

