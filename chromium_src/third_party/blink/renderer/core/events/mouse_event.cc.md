### match
```
...
/*
 * Copyright (C) 2001 Peter Kelly (pmk@post.com)
 * Copyright (C) 2001 Tobias Anton (anton@stud.fbi.fh-darmstadt.de)
 * Copyright (C) 2006 Samuel Weinig (sam.weinig@gmail.com)
 * Copyright (C) 2003, 2005, 2006, 2008 Apple Inc. All rights reserved.
 *
 * This library is free software; you can redistribute it and/or
 * modify it under the terms of the GNU Library General Public
 * License as published by the Free Software Foundation; either
 * version 2 of the License, or (at your option) any later version.
 *
 * This library is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
 * Library General Public License for more details.
 *
 * You should have received a copy of the GNU Library General Public License
 * along with this library; see the file COPYING.LIB.  If not, write to
 * the Free Software Foundation, Inc., 51 Franklin Street, Fifth Floor,
 * Boston, MA 02110-1301, USA.
 */
 #include "third_party/blink/renderer/core/events/mouse_event.h"
 
 >>> 
#include "third_party/blink/public/common/input/web_pointer_properties.h"

 ...
```
### patch
```
#include "third_party/blink/renderer/core/events/mouse_event.h"
#include "third_party/blink/renderer/bindings/core/v8/v8_mouse_event_init.h"
#include "third_party/blink/renderer/core/frame/local_dom_window.h"

```

### match
```
...
 namespace blink { ... 
 MouseEvent::MouseEvent(const AtomicString& event_type,
                       const MouseEventInit* initializer,
                       base::TimeTicks platform_time_stamp,
                       SyntheticEventType synthetic_event_type,
                       WebMenuSourceType menu_source_type,
                       LocalDOMWindow* fallback_dom_window)
    : UIEventWithKeyState(event_type, initializer, platform_time_stamp), >>> 
 screen_x_(initializer->screenX()) 
 , 
 screen_y_(initializer->screenY()) 
 ,  <<< ... 
movement_delta_(initializer->movementX(), initializer->movementY())
 ... ) ...  } ...
```
### patch
```
      screen_x_(initializer->screenX_ChromiumImpl()),
      screen_y_(initializer->screenY_ChromiumImpl()),

```

