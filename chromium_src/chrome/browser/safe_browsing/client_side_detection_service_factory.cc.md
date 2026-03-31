### match
```cpp
...
 
 namespace safe_browsing { ...   >>> 
 ClientSideDetectionService 
 * 
 ClientSideDetectionServiceFactory::GetForProfile 
 (  <<< 
Profile* profile
 ... ) ...  } ...  
```
### patch
```cpp
ClientSideDetectionService* ClientSideDetectionServiceFactory_ChromiumImpl::GetForProfile(

```

### match
```cpp
...
 
 namespace safe_browsing { ...   >>> 
 ClientSideDetectionServiceFactory 
 *
ClientSideDetectionServiceFactory::GetInstance() 
 { 
 static base::NoDestructor<ClientSideDetectionServiceFactory> instance;  <<< 
return instance.get();
 ... } ...  } ...  
```
### patch
```cpp
ClientSideDetectionServiceFactory_ChromiumImpl*
ClientSideDetectionServiceFactory_ChromiumImpl::GetInstance() {
  static base::NoDestructor<ClientSideDetectionServiceFactory_ChromiumImpl> instance;

```

### match
```cpp
...
 
 namespace safe_browsing { ...   >>> 
 ClientSideDetectionServiceFactory::ClientSideDetectionServiceFactory()  <<< 
: ProfileKeyedServiceFactory(
          "ClientSideDetectionService",
          ProfileSelections::Builder()
              .WithRegular(ProfileSelection::kOriginalOnly)
              // ChromeOS creates various profiles (login, lock screen...) that
              // do not display web content and thus do not need the
              // client side phishing detection
              .WithAshInternals(ProfileSelection::kNone)
              .Build())
 ... } ...  
```
### patch
```cpp
ClientSideDetectionServiceFactory_ChromiumImpl::ClientSideDetectionServiceFactory_ChromiumImpl()

```

### match
```cpp
...
>>>
 ProfileKeyedServiceFactory 
 (  <<< 
"ClientSideDetectionService"
 ... ) ...  
```
### patch
```cpp
    : ProfileKeyedServiceFactory(

```

### match
```cpp
...
 
 namespace safe_browsing { ... 
 std::unique_ptr<KeyedService>
  >>> 
 ClientSideDetectionServiceFactory::BuildServiceInstanceForBrowserContext 
 (  <<< 
content::BrowserContext* context
 ... ) ...  } ...  
```
### patch
```cpp
ClientSideDetectionServiceFactory_ChromiumImpl::BuildServiceInstanceForBrowserContext(

```

### match
```cpp
...
 
 namespace safe_browsing { ...   >>> 
 bool 
 ClientSideDetectionServiceFactory::ServiceIsCreatedWithBrowserContext 
 ()  <<<  ...} ...  
```
### patch
```cpp
bool ClientSideDetectionServiceFactory_ChromiumImpl::ServiceIsCreatedWithBrowserContext()

```

### match
```cpp
...
 
 namespace safe_browsing { ...   >>> 
 bool 
 ClientSideDetectionServiceFactory::ServiceIsNULLWhileTesting() const 
 {  <<< 
return true;
 ... } ...  } ...  
```
### patch
```cpp
bool ClientSideDetectionServiceFactory_ChromiumImpl::ServiceIsNULLWhileTesting() const {

```

### match
```cpp
...
 
 namespace safe_browsing { ... 
 
 bool ClientSideDetectionServiceFactory_ChromiumImpl::ServiceIsNULLWhileTesting() const { ... 
return true;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// static
ClientSideDetectionService* ClientSideDetectionServiceFactory::GetForProfile(
    Profile* profile) {
  return nullptr;
}

// static
ClientSideDetectionServiceFactory*
ClientSideDetectionServiceFactory::GetInstance() {
  return nullptr;
}


```

