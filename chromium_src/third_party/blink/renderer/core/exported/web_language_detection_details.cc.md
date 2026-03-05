### match
```
...
 namespace blink { ...   >>> 
 void 
 WebLanguageDetectionDetails::RecordAcceptLanguageAndXmlHtmlLangMetric 
 (  <<< ... 
const WebDocument& web_document
 ... ) ...  } ...  
```
### patch
```
void WebLanguageDetectionDetails::RecordAcceptLanguageAndXmlHtmlLangMetric(const WebDocument& web_document) {}
  void WebLanguageDetectionDetails::
      RecordAcceptLanguageAndXmlHtmlLangMetric_ChromiumImpl(

```

