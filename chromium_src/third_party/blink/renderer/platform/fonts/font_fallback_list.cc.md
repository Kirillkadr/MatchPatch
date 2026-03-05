### match
```
...
/*
 * Copyright (C) 2006 Apple Computer, Inc.  All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 * 1.  Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 * 2.  Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 * 3.  Neither the name of Apple Computer, Inc. ("Apple") nor the names of
 *     its contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY APPLE AND ITS CONTRIBUTORS "AS IS" AND ANY
 * EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
 * WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
 * DISCLAIMED. IN NO EVENT SHALL APPLE OR ITS CONTRIBUTORS BE LIABLE FOR ANY
 * DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
 * (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
 * LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
 * ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
 * (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF
 * THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
 #include "third_party/blink/renderer/platform/fonts/font_fallback_list.h"
 
 >>> 
#include "base/timer/elapsed_timer.h"

 ... 
```
### patch
```
#include "base/check.h"
#include "base/no_destructor.h"
#include "third_party/blink/renderer/platform/fonts/font_selector.h"
#include "third_party/blink/renderer/platform/wtf/text/atomic_string.h"

```

### match
```
...
 namespace blink { ... 
const ShapeResult& FontFallbackList::GetOrCreateEmphasisMarkShape(
    const Font& font,
    const AtomicString& mark) {
  const ShapeResult* cached_result = emphasis_mark_shape_.Get();
  if (mark == emphasis_mark_text_ && cached_result) {
    return *cached_result;
  }
  String mark16 = mark;
  // HarfBuzzShaper requires a 16-bit string for a vertical text.
  mark16.Ensure16Bit();
  cached_result = HarfBuzzShaper(mark16).Shape(&font, TextDirection::kLtr);
  emphasis_mark_text_ = mark;
  emphasis_mark_shape_ = cached_result;
  return *cached_result;
}
 } 
 // namespace blink 
 >>> 
 ... 
```
### patch
```
namespace brave {

namespace {

AllowFontFamilyCallback* GetAllowFontFamilyCallback() {
  static base::NoDestructor<AllowFontFamilyCallback> callback;
  return callback.get();
}

}  // namespace

void RegisterAllowFontFamilyCallback(AllowFontFamilyCallback callback) {
  DCHECK(GetAllowFontFamilyCallback()->is_null());
  *GetAllowFontFamilyCallback() = std::move(callback);
}

}  // namespace brave
```

