### match
```
...
 # ifndef ... 
#include <memory>

 #include <optional>
 
 >>> 
#include "base/byte_size.h"

 ... 
```
### patch
```
#include <optional>

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
WebGLContextAttributes* getContextAttributes() const;
 GLenum getError(); 
 >>> 
ScriptObject getExtension(ScriptState*, const String& name);
 ... } ...  
```
### patch
```
  ScriptObject getExtension_ChromiumImpl(ScriptState*, const String& name);

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
WebGLShaderPrecisionFormat* getShaderPrecisionFormat(GLenum shader_type,
                                                       GLenum precision_type);
 String getShaderSource(WebGLShader*); 
 >>> 
std::optional<Vector<String>> getSupportedExtensions();
 ... } ...  
```
### patch
```
  std::optional<Vector<String>> getSupportedExtensions_ChromiumImpl();

```

