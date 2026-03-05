### match
```
...
 # ifndef ... 
#define NET_BASE_HOST_PORT_PAIR_H_

 #include <stdint.h>
 
 >>> 
#include <optional>

 ... 
```
### patch
```
#include <compare>
#include <string>
#include <string_view>

```

### match
```
...
>>>
 class NET_EXPORT 
 HostPortPair 
 {  <<< ... 
public:
  HostPortPair();
 ... } ...  
```
### patch
```
class NET_EXPORT HostPortPair_ChromiumImpl {

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT HostPortPair_ChromiumImpl { ...   >>> 
 HostPortPair();  <<< ... } ...  } ...  
```
### patch
```
  HostPortPair_ChromiumImpl();

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT HostPortPair_ChromiumImpl { ... 
// If |in_host| represents an IPv6 address, it should not bracket the address.  >>> 
 HostPortPair(std::string_view in_host, uint16_t in_port) 
 ; 
 HostPortPair(const char* in_host, uint16_t in_port) 
 ; 
 HostPortPair(std::string&& in_host, uint16_t in_port) 
 ;  <<< ... 
// Creates a HostPortPair for the origin of |url|.
 ... } ...  } ...  
```
### patch
```
  HostPortPair_ChromiumImpl(std::string_view in_host, uint16_t in_port);
  HostPortPair_ChromiumImpl(const char* in_host, uint16_t in_port);
  HostPortPair_ChromiumImpl(std::string&& in_host, uint16_t in_port);

```

### match
```
...
;  >>> 
 // Creates a HostPortPair for the origin of |url|. 
 static HostPortPair FromURL(const GURL& url); 
 static 
 HostPortPair 
 FromSchemeHostPort 
 (  <<< ... 
const url::SchemeHostPort& scheme_host_port
 ... ) ...  
```
### patch
```
  // Creates a HostPortPair_ChromiumImpl for the origin of |url|.
  static HostPortPair_ChromiumImpl FromURL(const GURL& url);

  static HostPortPair_ChromiumImpl FromSchemeHostPort(

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT HostPortPair_ChromiumImpl { ... 
static HostPortPair_ChromiumImpl FromSchemeHostPort(
		const url::SchemeHostPort& scheme_host_port);  >>> 
 // Creates a HostPortPair from an IPEndPoint. 
 static HostPortPair FromIPEndPoint(const IPEndPoint& ipe);  <<< ... 
// Creates a HostPortPair from a string formatted in same manner as
 ... } ...  } ...  
```
### patch
```
  // Creates a HostPortPair_ChromiumImpl from an IPEndPoint.
  static HostPortPair_ChromiumImpl FromIPEndPoint(const IPEndPoint& ipe);

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT HostPortPair_ChromiumImpl { ... 
static HostPortPair_ChromiumImpl FromIPEndPoint(const IPEndPoint& ipe);  >>> 
 // Creates a HostPortPair from a string formatted in same manner as  <<< ... 
// ToString().
 ... } ...  } ...  
```
### patch
```

  // Creates a HostPortPair_ChromiumImpl from a string formatted in same manner as

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT HostPortPair_ChromiumImpl { ... 
// ToString().  >>> 
 static HostPortPair FromString(std::string_view str);  <<< ... 
// Nullopt if `value` is malformed to be deserialized to HostPortPair.
 ... } ...  } ...  
```
### patch
```
  static HostPortPair_ChromiumImpl FromString(std::string_view str);

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT HostPortPair_ChromiumImpl { ... 
static HostPortPair_ChromiumImpl FromString(std::string_view str);  >>> 
 // Nullopt if `value` is malformed to be deserialized to HostPortPair. 
 static std::optional<HostPortPair> FromValue(const base::Value& value); 
 friend bool operator==(const HostPortPair&, const HostPortPair&) = default; 
 friend auto operator<=>(const HostPortPair&, const HostPortPair&) = default;  <<< ... 
bool IsEmpty() const {
    return host_.empty() && port_ == 0;
  }
 ... } ...  } ...  
```
### patch
```
  // Nullopt if `value` is malformed to be deserialized to HostPortPair_ChromiumImpl.
  static std::optional<HostPortPair_ChromiumImpl> FromValue(const base::Value& value);

  friend bool operator==(const HostPortPair_ChromiumImpl&, const HostPortPair_ChromiumImpl&) = default;
  friend auto operator<=>(const HostPortPair_ChromiumImpl&, const HostPortPair_ChromiumImpl&) = default;

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT HostPortPair_ChromiumImpl { ... 
void set_port(uint16_t in_port) { port_ = in_port; }  >>> 
 // ToString() will convert the HostPortPair to "host:port".  If |host_| is an  <<< ... 
// IPv6 literal, it will add brackets around |host_|.
 ... } ...  } ...  
```
### patch
```
  // ToString() will convert the HostPortPair_ChromiumImpl to "host:port".  If |host_| is an

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT HostPortPair_ChromiumImpl { ... 
std::string host_;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```
class NET_EXPORT HostPortPair : public HostPortPair_ChromiumImpl {
 public:
  HostPortPair();
  HostPortPair(std::string_view in_host, uint16_t in_port);
  HostPortPair(std::string_view username,
               std::string_view password,
               std::string_view in_host,
               uint16_t in_port);
  HostPortPair(const HostPortPair&);
  ~HostPortPair();

  static HostPortPair FromURL(const GURL& url);
  static HostPortPair FromSchemeHostPort(
      const url::SchemeHostPort& scheme_host_port);
  static HostPortPair FromIPEndPoint(const IPEndPoint& ipe);
  static HostPortPair FromString(std::string_view str);
  static std::optional<HostPortPair> FromValue(const base::Value& value);

  const std::string& username() const { return username_; }
  const std::string& password() const { return password_; }

  void set_username(const std::string& username);
  void set_password(const std::string& password);

  std::strong_ordering operator<=>(const HostPortPair& other) const;
  bool operator==(const HostPortPair& other) const;
  bool Equals(const HostPortPair& other) const;

  std::string ToString() const;

 private:
  // NOLINTNEXTLINE(runtime/explicit)
  HostPortPair(const HostPortPair_ChromiumImpl& other);

  std::string username_;
  std::string password_;
};

```

