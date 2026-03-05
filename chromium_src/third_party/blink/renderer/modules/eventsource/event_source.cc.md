### match
```
...
 namespace blink { ...   >>> 
 void 
 EventSource::ConnectTimerFired(TimerBase*) 
 {  <<< ... 
Connect();
 ... } ...  } ...  
```
### patch
```
void EventSource::ConnectTimerFired_ChromiumImpl(TimerBase*) {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 EventSource::close() 
 {  <<< ... 
if (state_ == kClosed) {
    DCHECK(!loader_);
    return;
  }
 ... } ...  } ...  
```
### patch
```
void EventSource::close_ChromiumImpl() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 EventSource::DidFail(uint64_t, const ResourceError& error) 
 {  <<< ... 
DCHECK(loader_);
 ... } ...  } ...  
```
### patch
```
void EventSource::DidFail_ChromiumImpl(uint64_t, const ResourceError& error) {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 EventSource::DidFailRedirectCheck(uint64_t) 
 {  <<< ... 
DCHECK(loader_);
 ... } ...  } ...  
```
### patch
```
void EventSource::DidFailRedirectCheck_ChromiumImpl(uint64_t) {

```

### match
```
...
 namespace blink { ... 
 void EventSource::ContextDestroyed() { ...   >>> 
 close();  <<< ... } ...  } ...  
```
### patch
```
  close_ChromiumImpl();

```

### match
```
...
 namespace blink { ... 
 void EventSource::Trace(Visitor* visitor) const { ... 
EventSourceParser::Client::Trace(visitor);
 } 
 >>> 
 ... } ...  
```
### patch
```
void EventSource::ConnectTimerFired(TimerBase* timer_base) {
  BraveConnect();
}
void EventSource::BraveConnect() {
  if (base::FeatureList::IsEnabled(blink::features::kRestrictEventSourcePool)) {
    ExecutionContext* execution_context = GetExecutionContext();
    const bool is_extension = CommonSchemeRegistry::IsExtensionScheme(
        execution_context->GetSecurityOrigin()->Protocol().Ascii());
    if (!is_extension &&
        brave::GetBraveFarblingLevelFor(
            execution_context,
            ContentSettingsType::BRAVE_WEBCOMPAT_EVENT_SOURCE_POOL,
            BraveFarblingLevel::OFF) != BraveFarblingLevel::OFF) {
      event_source_in_use_tracker_ =
          ResourcePoolLimiter::GetInstance().IssueResourceInUseTracker(
              execution_context,
              ResourcePoolLimiter::ResourceType::kEventSource);
      if (!event_source_in_use_tracker_) {
        AbortConnectionAttempt();
        return;
      }
    }
  }
  Connect();
}

void EventSource::MaybeResetEventSourceInUseTracker() {
  if (base::FeatureList::IsEnabled(blink::features::kRestrictEventSourcePool)) {
    if (event_source_in_use_tracker_ != nullptr) {
      event_source_in_use_tracker_.reset();
    }
  }
}

void EventSource::close() {
  close_ChromiumImpl();
  MaybeResetEventSourceInUseTracker();
}

void EventSource::DidFail(uint64_t identifier, const ResourceError& error) {
  DidFail_ChromiumImpl(identifier, error);
  if (state_ == kClosed) {
    MaybeResetEventSourceInUseTracker();
  }
}

void EventSource::DidFailRedirectCheck(uint64_t identifier) {
  DidFailRedirectCheck_ChromiumImpl(identifier);
  if (state_ == kClosed) {
    MaybeResetEventSourceInUseTracker();
  }
}

```

