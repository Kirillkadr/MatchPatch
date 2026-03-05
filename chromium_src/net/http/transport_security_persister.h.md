### match
```
...
 # ifndef ... 
 namespace net { ... 
// background_runner is the task runner this class should use internally to
 // perform file IO, and can optionally be associated with a different thread. 
 >>> 
class NET_EXPORT TransportSecurityPersister
    : public TransportSecurityState::Delegate,
      public base::ImportantFileWriter::DataSerializer {
 public:
  // Create a TransportSecurityPersister with state |state| on background runner
  // |background_runner|. |data_path| points to the file to hold the transport
  // security state data on disk.
  TransportSecurityPersister(
      TransportSecurityState* state,
      const scoped_refptr<base::SequencedTaskRunner>& background_runner,
      const base::FilePath& data_path);
 ... } ...  } ...  
```
### patch
```

// Use upstream version of TransportSerurityState to reference
// TransportSecurityState::Delegate without build issues.
#define TransportSecurityState TransportSecurityState_ChromiumImpl

```

### match
```
...
 # ifndef ... 
;
 } 
 // namespace net 
 >>> 
 ... 
```
### patch
```
#undef TransportSecurityState

```

