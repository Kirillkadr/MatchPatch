### match
```
...
 namespace blink { ...   >>> 
 void 
 ReportingObserver::QueueReport(Report* report) 
 {  <<< ... 
if (!ObservedType(report->type()))
    return;
 ... } ...  } ...  
```
### patch
```
void ReportingObserver::QueueReport_Unused(Report* report) {

```

### match
```
...
 namespace blink { ... 
 void ReportingObserver::Trace(Visitor* visitor) const { ... 
ExecutionContextClient::Trace(visitor);
 } 
 >>> 
 ... } ...  
```
### patch
```
// Don't add reports. We previously used to disable ReportingObserver in
// Brave, but for webcompat reasons, we now just no-op it. This makes
// takeRecords() always return an empty list.
void ReportingObserver::QueueReport(Report* report) {}

```

