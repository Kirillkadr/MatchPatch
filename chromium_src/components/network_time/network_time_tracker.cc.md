### match
```cpp
...
 
void NetworkTimeTracker::NotifyObservers() {
  // Don't notify if the current state is not NETWORK_TIME_AVAILABLE.
  base::Time unused;
  auto res = GetNetworkTime(&unused, nullptr);
  if (res != NETWORK_TIME_AVAILABLE) {
    return;
  }
  TimeTracker::TimeTrackerState state = tracker_->GetStateAtCreation();
  for (NetworkTimeObserver& obs : observers_) {
    obs.OnNetworkTimeChanged(state);
  }
}
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kNetworkTimeServiceQuerying, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

