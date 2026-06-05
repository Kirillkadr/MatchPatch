### match
```cpp
...
 
 namespace policy { ... 
// Number of source types. Has to be the last element.
>>> 
 POLICY_SOURCE_COUNT 
<<< 
...} ...  
```
### patch
```cpp
  POLICY_SOURCE_COUNT POLICY_SOURCE_BRAVE, POLICY_SOURCE_COUNT

```

### match
```cpp
...
 
 namespace policy { ... 
// The policy was set through remapping or debugging.
>>> 
 kEnterpriseDefault 
 , 
<<< 
// The policy was set by command line flag for testing purposes.
 ... } ...  
```
### patch
```cpp
  kBravePriority, kEnterpriseDefault,

```

### match
```cpp
...
 
 namespace policy { ... 
 } 
 // namespace policy 
 >>> 
 ... 
```
### patch
```cpp
static_assert(policy::POLICY_SOURCE_BRAVE == 10,
              "POLICY_SOURCE_BRAVE must equal 10");

```

