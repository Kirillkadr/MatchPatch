### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT TimeClamper { ...   >>> 
 static constexpr int kCoarseResolutionMicroseconds = 100; 
 static constexpr int kFineResolutionMicroseconds = 5;  <<< ... 
TimeClamper();
 ... } ...  } ...  
```
### patch
```
  static constexpr int kCoarseResolutionMicroseconds_ChromiumImpl = 100;
  static constexpr int kFineResolutionMicroseconds_ChromiumImpl = 5;
  static int CoarseResolutionMicroseconds();
  static int FineResolutionMicroseconds();
  static double MaybeRoundMilliseconds(double value);
  static base::TimeDelta MaybeRoundTimeDelta(base::TimeDelta value);
  int dummy = 5;

```

