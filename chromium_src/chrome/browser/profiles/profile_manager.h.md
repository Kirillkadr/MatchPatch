### match
```cpp
...
 
 # ifndef ... 
 
 class ProfileManager : public Profile::Delegate { ... 
// Note: The list returned might contain on-the-record irregular profiles
 // like the System profile. 
 >>> 
static std::vector<Profile*> GetLastOpenedProfiles();
 ... } ...
```
### patch
```cpp
static std::vector<Profile*> GetLastOpenedProfiles_ChromiumImpl();

```

### match
```cpp
...
 
 # ifndef ... 
// Returns total number of profiles available on this machine.  >>> 
 size_t GetNumberOfProfiles();  <<< 
// Asynchronously loads an existing profile given its |profile_base_name|
 ...
```
### patch
```cpp
size_t virtual GetNumberOfProfiles();

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ProfileManager : public Profile::Delegate { ...   >>> 
 bool 
 LoadProfileByPath 
 ( 
 const base::FilePath& profile_path 
 ,  <<< 
bool incognito
 ... ) ...  } ...
```
### patch
```cpp
bool  virtual LoadProfileByPath(const base::FilePath& profile_path,

```

### match
```cpp
...
 
 # ifndef ... 
// avatar values.  >>> 
 void InitProfileUserPrefs(Profile* profile);  <<< 
// Register and add testing profile to the ProfileManager. Use ONLY in tests.
 ...
```
### patch
```cpp
void  virtual InitProfileUserPrefs(Profile* profile);

```

### match
```cpp
...
// Returns whether |path| is allowed for profile creation.  >>> 
 bool IsAllowedProfilePath(const base::FilePath& path) const;  <<< 
 ...
```
### patch
```cpp
bool  virtual IsAllowedProfilePath(const base::FilePath& path) const;

```

### match
```cpp
...
 
 # ifndef ... 
// Public so that `ProfileManagerAndroid` can call it.  >>> 
 void SetProfileAsLastUsed(Profile* last_active);  <<< 
// Asynchronous loading is initially deferred until the application main loop
 ...
```
### patch
```cpp
void  virtual SetProfileAsLastUsed(Profile* last_active);

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ProfileManager : public Profile::Delegate { ... 
 friend class TestingProfileManager; 
 >>> 
FRIEND_TEST_ALL_PREFIXES(ProfileManagerBrowserTest, DeleteAllProfiles);
 ... } ...
```
### patch
```cpp
friend class BraveProfileManager;

```

### match
```cpp
...
 
 # ifndef ... 
void DoFinalInit(ProfileInfo* profile_info, bool go_off_the_record);  >>> 
 void DoFinalInitForServices(Profile* profile, bool go_off_the_record);  <<< 
void DoFinalInitLogging(Profile* profile);
 ...
```
### patch
```cpp
void  virtual DoFinalInitForServices(Profile* profile, bool go_off_the_record);

```

### match
```cpp
...
 
   >>> 
 void SetNonPersonalProfilePrefs(Profile* profile);  <<< 
void SaveActiveProfiles();
 ...
```
### patch
```cpp
void  virtual SetNonPersonalProfilePrefs(Profile* profile);

```

