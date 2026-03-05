### match
```
...
 namespace blink { ... 
 namespace bindings { ... 
 void IDLMemberInstaller::InstallExposedConstructs(
    v8::Isolate* isolate,
    const DOMWrapperWorld& world,
    v8::Local<v8::Object> instance_object,
    v8::Local<v8::Object> prototype_object,
    v8::Local<v8::Object> interface_object,
    v8::Local<v8::Signature> signature,
    base::span<const ExposedConstructConfig> configs) { ... 
for (const auto& config : configs) {
    instance_object
        ->SetLazyDataProperty(context, V8AtomicString(isolate, config.name),
                              config.callback, v8::Local<v8::Value>(),
                              v8::DontEnum,
                              v8::SideEffectType::kHasNoSideEffect)
        .ToChecked();
  }
 } 
 >>> 
 ... } ...  } ...  
```
### patch
```
namespace {
bool IsConnectionConfig(const IDLMemberInstaller::AttributeConfig& config) {
  constexpr std::string_view kConnection = "connection";
  return kConnection == config.property_name;
}

}  // namespace

// static
template <>
PLATFORM_EXPORT void IDLMemberInstaller::BraveInstallAttributes<
    BraveNavigatorAttributeInstallerTrait>(
    v8::Isolate* isolate,
    const DOMWrapperWorld& world,
    v8::Local<v8::Template> instance_template,
    v8::Local<v8::Template> prototype_template,
    v8::Local<v8::Template> interface_template,
    v8::Local<v8::Signature> signature,
    const char* interface_name,
    base::span<const AttributeConfig> configs) {
  const bool connection_attribute_enabled = base::FeatureList::IsEnabled(
      blink::features::kNavigatorConnectionAttribute);
  for (const auto& config : configs) {
    if (!connection_attribute_enabled && IsConnectionConfig(config)) {
      continue;
    }
    InstallAttribute(isolate, world, instance_template, prototype_template,
                     interface_template, signature, interface_name, config);
  }
}

// static
template <>
PLATFORM_EXPORT void IDLMemberInstaller::BraveInstallAttributes<
    BraveNavigatorAttributeInstallerTrait>(
    v8::Isolate* isolate,
    const DOMWrapperWorld& world,
    v8::Local<v8::Object> instance_object,
    v8::Local<v8::Object> prototype_object,
    v8::Local<v8::Object> interface_object,
    v8::Local<v8::Signature> signature,
    const char* interface_name,
    base::span<const AttributeConfig> configs) {
  const bool connection_attribute_enabled = base::FeatureList::IsEnabled(
      blink::features::kNavigatorConnectionAttribute);
  v8::Local<v8::Context> context = isolate->GetCurrentContext();
  for (const auto& config : configs) {
    if (!connection_attribute_enabled && IsConnectionConfig(config)) {
      continue;
    }
    InstallAttribute(isolate, context, world, instance_object, prototype_object,
                     interface_object, signature, interface_name, config);
  }
}

```

