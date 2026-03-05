### match
```
...
 namespace blink { ...   >>> 
 void 
 FrameTree::ExperimentalSetNulledName() 
 {  <<< ... 
experimental_set_nulled_name_ = true;
 ... } ...  } ...  
```
### patch
```
void FrameTree::ExperimentalSetNulledName_ChromiumImpl() {

```

### match
```
...
 namespace blink { ... 
 void FrameTree::Trace(Visitor* visitor) const { ... 
visitor->Trace(this_frame_);
 } 
 >>> 
 ... } ...  
```
### patch
```
void FrameTree::ExperimentalSetNulledName() {
  SetName(g_null_atom, kReplicate);
  ExperimentalSetNulledName_ChromiumImpl();
}

```

