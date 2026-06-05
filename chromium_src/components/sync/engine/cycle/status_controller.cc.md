### match
```cpp
...
 
 namespace syncer { ... 
 
 int StatusController::num_server_conflicts() const { ... 
return model_neutral_.num_server_conflicts;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
const std::string& StatusController::get_last_server_error_message() const {
  return model_neutral_.last_server_error_message;
}

void StatusController::set_last_server_error_message(
    const std::string& message) {
  model_neutral_.last_server_error_message = message;
}

```

