### match
```cpp
...
 
 # ifndef ... 
 
 namespace download { ... 
COMPONENTS_DOWNLOAD_EXPORT scoped_refptr<base::SequencedTaskRunner>
GetDownloadTaskRunner();
 // Sets the task runner used to perform network IO. 
 >>> 
COMPONENTS_DOWNLOAD_EXPORT void SetIOTaskRunner(
    const scoped_refptr<base::SingleThreadTaskRunner>& task_runner);
 ... } ...  
```
### patch
```cpp
COMPONENTS_DOWNLOAD_EXPORT void ClearIOTaskRunnerForTesting();

```

