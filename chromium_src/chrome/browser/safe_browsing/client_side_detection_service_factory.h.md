### match
```cpp
...
 
 # ifndef ... 
 
 namespace safe_browsing { ...   >>> 
 class 
 ClientSideDetectionServiceFactory 
 : public ProfileKeyedServiceFactory 
 {  <<< 
public
 ... } ...  } ...  
```
### patch
```cpp
class ClientSideDetectionServiceFactory_ChromiumImpl : public ProfileKeyedServiceFactory {

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace safe_browsing { ... 
// Get the singleton instance.  >>> 
 static ClientSideDetectionServiceFactory* GetInstance();  <<< 
ClientSideDetectionServiceFactory(const ClientSideDetectionServiceFactory&) =
      delete;
 ... } ...  
```
### patch
```cpp
  static ClientSideDetectionServiceFactory_ChromiumImpl* GetInstance();

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace safe_browsing { ... 
 
 class ClientSideDetectionServiceFactory_ChromiumImpl : public ProfileKeyedServiceFactory { ...   >>> 
 ClientSideDetectionServiceFactory(const ClientSideDetectionServiceFactory&) 
 =  <<<  ...} ...  } ...  
```
### patch
```cpp

  ClientSideDetectionServiceFactory_ChromiumImpl(const ClientSideDetectionServiceFactory_ChromiumImpl&) =

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace safe_browsing { ... 
 
 class ClientSideDetectionServiceFactory_ChromiumImpl : public ProfileKeyedServiceFactory { ... 
ClientSideDetectionServiceFactory_ChromiumImpl(const ClientSideDetectionServiceFactory_ChromiumImpl&) =
		delete;  >>> 
 ClientSideDetectionServiceFactory& operator=(
      const ClientSideDetectionServiceFactory&) = delete;  <<< 
private
 ... } ...  } ...  
```
### patch
```cpp
  ClientSideDetectionServiceFactory_ChromiumImpl& operator=(
      const ClientSideDetectionServiceFactory_ChromiumImpl&) = delete;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace safe_browsing { ... 
ClientSideDetectionServiceFactory_ChromiumImpl& operator=(
		      const ClientSideDetectionServiceFactory_ChromiumImpl&) = delete;  >>> 
 private 
 : 
 friend base::NoDestructor<ClientSideDetectionServiceFactory>; 
 ClientSideDetectionServiceFactory(); 
 ~ClientSideDetectionServiceFactory() override = default;  <<< 
// BrowserContextKeyedServiceFactory:
 ... } ...  
```
### patch
```cpp
 private:
  friend base::NoDestructor<ClientSideDetectionServiceFactory_ChromiumImpl>;

  ClientSideDetectionServiceFactory_ChromiumImpl();
  ~ClientSideDetectionServiceFactory_ChromiumImpl() override = default;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace safe_browsing { ... 
 
 class ClientSideDetectionServiceFactory_ChromiumImpl : public ProfileKeyedServiceFactory { ... 
bool ServiceIsNULLWhileTesting() const override;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
class ClientSideDetectionServiceFactory {
 public:
  static ClientSideDetectionService* GetForProfile(Profile* profile);

  // Get the singleton instance.
  static ClientSideDetectionServiceFactory* GetInstance();
};

```

