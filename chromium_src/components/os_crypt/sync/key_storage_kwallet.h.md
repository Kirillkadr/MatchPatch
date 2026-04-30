### match
```cpp
...
 
 # ifndef ... 
// Create Chrome's folder in the wallet, if it doesn't exist.
 bool InitFolder(); 
 >>> 
// Generates a new 16-byte key, stores it in KWallet and returns the key
 ... 
```
### patch
```cpp
  const char* GetFolderName();
  const char* GetKeyName();

```

