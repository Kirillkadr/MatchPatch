### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT DocumentLoadTiming final { ... 
public:
  explicit DocumentLoadTiming(DocumentLoader&);
 base::TimeDelta MonotonicTimeToZeroBasedDocumentTime(base::TimeTicks) const; 
 >>> 
int64_t ZeroBasedDocumentTimeToMonotonicTime(double dom_event_time) const;
 ... } ...  } ...  
```
### patch
```
  base::TimeDelta MonotonicTimeToZeroBasedDocumentTime_ChromiumImpl(base::TimeTicks) const;

```

