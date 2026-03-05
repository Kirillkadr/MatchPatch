### match
```
...
      >>> frame_->Tree().ExperimentalSetNulledName(); <<<
      ...
```
### patch
```
    GetName();                                                          
  if (!frame_->origin_for_clear_window_name_check_.IsSameOriginWith(  
          frame_->DomWindow()->GetSecurityOrigin()->ToUrlOrigin())) { 
    frame_->Tree().ExperimentalSetNulledName();            
  }                                                                   
  frame_->origin_for_clear_window_name_check_ = url::Origin();

```

