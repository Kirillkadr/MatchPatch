### match
```cpp
...
 
 # ifndef ... 
// ID used by the Incognito and Guest profiles.
 static const OTRProfileID PrimaryID(); 
 >>> 
// Creates a unique OTR profile id with the given profile id prefix.
 ... 
```
### patch
```cpp
  static OTRProfileID CreateUniqueForSearchBackupResults();
  bool IsSearchBackupResults() const;
  static const OTRProfileID AIChatCodeExecutionID();
  friend class TorProfileManager;
  static const OTRProfileID TorID();

```

### match
```cpp
...
 
 # ifndef ... 
 
 class Profile : public content::BrowserContext { ... 
virtual bool HasAnyOffTheRecordProfile() = 0;
 // True if the primary OffTheRecord profile exists. 
 >>> 
bool HasPrimaryOTRProfile();
 ... } ...  
```
### patch
```cpp
  bool IsTor() const override;
  bool IsAIChatAgent() const override;

```

### match
```cpp
...
 
 # ifndef ... 
 
 class Profile : public content::BrowserContext { ... 
// Returns whether it is an Incognito profile. An Incognito profile is an
 // off-the-record profile that is used for incognito mode. 
 >>> 
bool IsIncognitoProfile() const;
 ... } ...  
```
### patch
```cpp
  bool IsIncognitoProfile_ChromiumImpl() const;

```

### match
```cpp
...
 
 # ifndef ... 
 
 class Profile : public content::BrowserContext { ... 
// Returns true if this is a primary OffTheRecord profile, which covers the
 // OffTheRecord profile used for incognito mode and guest sessions. 
 >>> 
bool IsPrimaryOTRProfile() const;
 ... } ...  
```
### patch
```cpp
  bool IsPrimaryOTRProfile_ChromiumImpl() const;

```

