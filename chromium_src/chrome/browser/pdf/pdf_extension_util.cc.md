### match
```cpp
...
 
 namespace pdf_extension_util { ...   >>> 
 std::string 
 GetManifest() 
 {  <<< 
#if BUILDFLAG(GOOGLE_CHROME_BRANDING)
  static constexpr char kExtensionName[] = "Chrome PDF Viewer";
#else
  static constexpr char kExtensionName[] = "Chromium PDF Viewer";
#endif
 ... } ...  } ...
```
### patch
```cpp
std::string GetManifest_ChromiumImpl() {

```

### match
```cpp
...
 if (glic::GlicEnabling::IsTrustFirstOnboardingEnabledForProfile(profile)) {
    return true;
  }

  return false;
}
 >>> 
 ...
```
### patch
```cpp
std::string GetManifest() {
  std::string manifest_contents =
      pdf_extension_util::GetManifest_ChromiumImpl();
  base::ReplaceFirstSubstringAfterOffset(
      &manifest_contents, 0, "Chromium PDF Viewer", "Chrome PDF Viewer");
  return manifest_contents;
}

```

