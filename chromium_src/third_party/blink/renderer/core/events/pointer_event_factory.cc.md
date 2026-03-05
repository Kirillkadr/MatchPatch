### match
```
...
 namespace blink { ... 
 PointerEvent* PointerEventFactory::CreatePointerEventFrom(
    PointerEvent* pointer_event,
    const AtomicString& type,
    EventTarget* related_target) { ... 
pointer_event_init->setHeight(pointer_event->height());  >>> 
 pointer_event_init->setScreenX(pointer_event->screenX()); 
 pointer_event_init->setScreenY(pointer_event->screenY());  <<< ... 
pointer_event_init->setClientX(pointer_event->clientX());
 ... } ...  } ...  
```
### patch
```
  pointer_event_init->setScreenX(pointer_event->screenX_ChromiumImpl());
  pointer_event_init->setScreenY(pointer_event->screenY_ChromiumImpl());

```

