### match
```cpp
...
 
 namespace variations { ... 
 
 void UpdateCorsExemptHeaderForOmniboxAutofocus(
    network::mojom::NetworkContextParams* params) { ... 
// BUILDFLAG(IS_ANDROID)
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kReportOmniboxAutofocusHeader, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

