### match
```
...
 /*
    Copyright (C) 2010 Rob Buis <rwlbuis@gmail.com>
    Copyright (C) 2011 Cosmin Truta <ctruta@gmail.com>
    Copyright (C) 2012 University of Szeged
    Copyright (C) 2012 Renata Hodovan <reni@webkit.org>

    This library is free software; you can redistribute it and/or
    modify it under the terms of the GNU Library General Public
    License as published by the Free Software Foundation; either
    version 2 of the License, or (at your option) any later version.

    This library is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
    Library General Public License for more details.

    You should have received a copy of the GNU Library General Public License
    along with this library; see the file COPYING.LIB.  If not, write to
    the Free Software Foundation, Inc., 51 Franklin Street, Fifth Floor,
    Boston, MA 02110-1301, USA.
*/ 
 >>> 
#include "third_party/blink/renderer/core/svg/svg_resource_document_content.h"

 ... 
```
### patch
```
#include "third_party/blink/renderer/core/svg/svg_resource_document_content.h"
#include "brave/components/brave_page_graph/common/buildflags.h"
#include "third_party/blink/renderer/core/dom/dom_node_ids.h"
#include "third_party/blink/renderer/core/svg/graphics/svg_image_chrome_client.h"

```

### match
```
...
 namespace blink { ... 
 class SVGResourceDocumentContent::ChromeClient final
    : public IsolatedSVGChromeClient { ... 
 void ChromeDestroyed() override { content_.Clear(); } 
 >>> 
void InvalidateContainer() override { content_->ContentChanged(); }
 ... } ...  } ...  
```
### patch
```

#if BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)
  void DOMNodeId InitiatorDomNodeId() const override {
    return content_->initiator_dom_node_id();
  }
  void InvalidateContainer(__VA_ARGS__); }
#endif  // BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)


```

