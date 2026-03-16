### match
```
...
 # ifndef ... 
 namespace 
 base 
 { 
 >>> 
class TaskRunner
 ... } ...  
```
### patch
```
class TestLauncher;
using TestLauncher_BraveImpl = TestLauncher;

```

### match
```
...
 # ifndef ... 
 namespace base { ...   >>> 
 class 
 TestLauncher 
 {  <<< ... 
public
 ... } ...  } ...  
```
### patch
```
class TestLauncher_ChromiumImpl {

```

### match
```
...
 class TestLauncher_ChromiumImpl { ...   >>> 
 TestLauncher 
 ( 
 TestLauncherDelegate* launcher_delegate 
 ,  <<< ... 
size_t parallel_jobs
 ... ) ...  } ...  
```
### patch
```
  TestLauncher_ChromiumImpl(TestLauncherDelegate* launcher_delegate,

```

### match
```
...
 # ifndef ... 
 namespace base { ... 
 class TestLauncher_ChromiumImpl { ... 
TestLauncher_ChromiumImpl(TestLauncherDelegate* launcher_delegate,
		size_t parallel_jobs,
               size_t retry_limit = 1U);  >>> 
 TestLauncher(const TestLauncher&) = delete; 
 TestLauncher& operator=(const TestLauncher&) = delete;  <<< ... 
// virtual to mock in testing.
 ... } ...  } ...  
```
### patch
```
  TestLauncher_ChromiumImpl(const TestLauncher_ChromiumImpl&) = delete;
  TestLauncher_ChromiumImpl& operator=(const TestLauncher_ChromiumImpl&) = delete;

```

### match
```
...
 # ifndef ... 
 namespace base { ... 
 class TestLauncher_ChromiumImpl { ... 
// virtual to mock in testing.  >>> 
 virtual ~TestLauncher();  <<< ... 
// Runs the launcher. Must be called at most once.
 ... } ...  } ...  
```
### patch
```
  virtual ~TestLauncher_ChromiumImpl();

```

### match
```
...
 # ifndef ... 
 namespace base { ... 
// Called when a test has finished running.  >>> 
 void OnTestFinished(const TestResult& result);  <<< ... 
// Returns true if child test processes should have dedicated temporary
 ... } ...  
```
### patch
```
  friend TestLauncher_BraveImpl;
  virtual const TestResult& OnTestResult(const TestResult& result) = 0; 
  virtual void OnTestFinished(const TestResult& result);

```

### match
```
...
 # ifndef ... 
 namespace base { ... 
// Saves test results summary as JSON if requested from command line.  >>> 
 void MaybeSaveSummaryAsJSON(const std::vector<std::string>& additional_tags);  <<< ... 
// Called when a test iteration is finished.
 ... } ...  
```
### patch
```
  virtual void MaybeSaveSummaryAsJSON(const std::vector<std::string>& additional_tags);

```

### match
```
...
 # ifndef ... 
 namespace base { ... 
// retain fatal messages. Exposed for testing only.
 std::string TruncateSnippetFocused(std::string_view snippet, size_t byte_limit); 
 >>> 
 ... } ...  
```
### patch
```
class TeamcityReporter;

class TestLauncher : public TestLauncher_ChromiumImpl {
 public:
  TestLauncher(TestLauncherDelegate* launcher_delegate,
               size_t parallel_jobs,
               size_t retry_limit = 1U);
  ~TestLauncher() override;

  void OnTestFinished(const TestResult& result) override;

 private:
  void CreateAndStartThreadPool(size_t num_parallel_jobs) override;
  const TestResult& OnTestResult(const TestResult& result) override;
  void MaybeSaveSummaryAsJSON(
      const std::vector<std::string>& additional_tags) override;

  std::unique_ptr<TeamcityReporter> teamcity_reporter_;
};


```

