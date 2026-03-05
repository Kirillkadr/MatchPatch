### match
```
...
 namespace blink { ... 
 void HTMLLinkElement::MaybeHandlePaymentLink() { ... 
#if BUILDFLAG(IS_ANDROID)
  KURL payment_link = GetNonEmptyURLAttribute(html_names::kHrefAttr);
  if (rel_attribute_.IsFacilitatedPayment() && !payment_link.IsEmpty() &&
      isConnected() && GetDocument().IsInOutermostMainFrame() &&
      RuntimeEnabledFeatures::PaymentLinkDetectionEnabled()) {
    GetDocument().HandlePaymentLink(payment_link);
  }
#endif
 } 
 >>> 
 ... } ...  
```
### patch
```
HTMLLinkElement* HTMLLinkElement::GetOwner() {
  return this;
}

```

