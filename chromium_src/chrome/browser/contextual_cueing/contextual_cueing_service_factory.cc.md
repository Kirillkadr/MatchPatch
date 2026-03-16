### match
```
...
 namespace 
 contextual_cueing 
 { 
 >>> 
// static
 ... } ...  
```
### patch
```

// static
ContextualCueingService* ContextualCueingServiceFactory::GetForProfile(
    Profile* profile) {
  return nullptr;
}

// static
ContextualCueingServiceFactory* ContextualCueingServiceFactory::GetInstance() {
  static base::NoDestructor<ContextualCueingServiceFactory> instance;
  return instance.get();
}

ContextualCueingServiceFactory::ContextualCueingServiceFactory()
    : ProfileKeyedServiceFactory("ContextualCueingService",
                                 ProfileSelections::BuildNoProfilesSelected()) {
}

ContextualCueingServiceFactory::~ContextualCueingServiceFactory() = default;

std::unique_ptr<KeyedService>
ContextualCueingServiceFactory::BuildServiceInstanceForBrowserContext(
    content::BrowserContext* context) const {
  return nullptr;
}

bool ContextualCueingServiceFactory::ServiceIsCreatedWithBrowserContext()
    const {
  return true;
}

bool ContextualCueingServiceFactory::ServiceIsNULLWhileTesting() const {
  return true;
}


```

