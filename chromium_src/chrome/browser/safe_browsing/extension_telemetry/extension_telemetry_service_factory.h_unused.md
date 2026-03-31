### match
```cpp
...
 
 # ifndef ... 
 
 namespace safe_browsing { ... 
 
 class ExtensionTelemetryServiceFactory : public ProfileKeyedServiceFactory { ... 
bool ServiceIsNULLWhileTesting() const override;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
class ExtensionTelemetryService;

class ExtensionTelemetryServiceFactory : public ProfileKeyedServiceFactory {
 public:
  static ExtensionTelemetryService* GetForProfile(Profile* profile);

  // Get the singleton instance.
  static ExtensionTelemetryServiceFactory* GetInstance();

  ExtensionTelemetryServiceFactory(const ExtensionTelemetryServiceFactory&) =
      delete;
  ExtensionTelemetryServiceFactory& operator=(
      const ExtensionTelemetryServiceFactory&) = delete;

  std::unique_ptr<KeyedService> BuildServiceInstanceForBrowserContext(
      content::BrowserContext* context) const override;

 private:
  friend class base::NoDestructor<ExtensionTelemetryServiceFactory>;

  ExtensionTelemetryServiceFactory();
  ~ExtensionTelemetryServiceFactory() override = default;

  // BrowserContextKeyedServiceFactory:
  bool ServiceIsCreatedWithBrowserContext() const override;
  bool ServiceIsNULLWhileTesting() const override;
};


```

