### match
```cpp

...
// found in the LICENSE file.
 #include "ui/views/input_event_activation_protector.h"
 
 >>> 
#include "base/command_line.h"

 ...
 ```  
### patch
```cpp

#include "ui/views/input_event_activation_protector.h"
```
### match
```cpp

...
>>>
 namespace 
 views 
 { 
 >>> 
InputEventActivationProtector::InputEventActivationProtector() {
  WindowsStationarityMonitor::GetInstance()->AddObserver(this);
}
 ... } ...
 ```    
### patch
```cpp

void InputEventActivationProtector::IgnoreNextWindowStationaryStateChanged() {
  ignore_next_window_stationary_state_changed_ = true;
}
void InputEventActivationProtector::OnWindowStationaryStateChanged() {
  if (ignore_next_window_stationary_state_changed_) {
    ignore_next_window_stationary_state_changed_ = false;
    return;
  }
  OnWindowStationaryStateChanged_ChromiumImpl();
}
```