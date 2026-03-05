### match
```
...
/*
 * Copyright (C) 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012 Apple Inc.
 * All rights reserved.
 * Copyright (C) 2008, 2010 Nokia Corporation and/or its subsidiary(-ies)
 * Copyright (C) 2007 Alp Toker <alp@atoker.com>
 * Copyright (C) 2008 Eric Seidel <eric@webkit.org>
 * Copyright (C) 2008 Dirk Schulze <krit@webkit.org>
 * Copyright (C) 2010 Torch Mobile (Beijing) Co. Ltd. All rights reserved.
 * Copyright (C) 2012, 2013 Intel Corporation. All rights reserved.
 * Copyright (C) 2013 Adobe Systems Incorporated. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 * 1. Redistributions of source code must retain the above copyright
 *    notice, this list of conditions and the following disclaimer.
 * 2. Redistributions in binary form must reproduce the above copyright
 *    notice, this list of conditions and the following disclaimer in the
 *    documentation and/or other materials provided with the distribution.
 *
 * THIS SOFTWARE IS PROVIDED BY APPLE COMPUTER, INC. ``AS IS'' AND ANY
 * EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
 * IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL APPLE COMPUTER, INC. OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY
 * OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
 * (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
 * OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
 #include "third_party/blink/renderer/modules/canvas/canvas2d/canvas_rendering_context_2d.h"
 
 >>> 
#include <stddef.h>

 ... 
```
### patch
```
#include "brave/third_party/blink/renderer/core/farbling/brave_session_cache.h"

```

### match
```
...
 namespace blink { ...   >>> 
 ImageData 
 * 
 CanvasRenderingContext2D::getImageDataInternal 
 (  <<< ... 
int sx
 ... ) ...  } ...  
```
### patch
```
ImageData* CanvasRenderingContext2D::getImageDataInternal_Unused(

```

### match
```
...
 namespace blink { ... 
 void CanvasRenderingContext2D::SetCanvas2DResourceProviderForTesting(
    std::unique_ptr<CanvasResourceProvider> provider,
    const gfx::Size& size) { ... 
ReplaceResourceProvider(std::move(provider));
 } 
 >>> 
 ... } ...  
```
### patch
```
ImageData* CanvasRenderingContext2D::getImageDataInternal(
    ScriptState* script_state,
    int sx,
    int sy,
    int sw,
    int sh,
    ImageDataSettings* image_data_settings,
    ExceptionState& exception_state) {
  return BaseRenderingContext2D::getImageDataInternal(
      script_state, sx, sy, sw, sh, image_data_settings, exception_state);
}

```

