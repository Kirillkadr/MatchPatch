### match
```
...
NET_ERROR(BLOB_REFERENCED_FILE_UNAVAILABLE, -906)

// CAUTION: Before adding errors here, please check the ranges of errors written
// in the top of this file.

// LINT.ThenChange(
//      //tools/metrics/histograms/enums.xml:HTTPResponseAndNetErrorCodes,
//      //tools/metrics/histograms/enums.xml:NetErrorCodes,

 // ) 
 >>> 
 ... 
```
### patch
```
// NOLINT(build/header_guard)
// no-include-guard-because-multiply-included
NET_ERROR(ENS_OFFCHAIN_LOOKUP_NOT_SELECTED, -10004)

```

