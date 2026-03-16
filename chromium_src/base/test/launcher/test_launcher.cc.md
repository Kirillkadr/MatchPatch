### match
```
...
#include "third_party/abseil-cpp/absl/container/flat_hash_map.h"

 #include "third_party/abseil-cpp/absl/container/flat_hash_set.h"
 
 >>> 
#if BUILDFLAG(IS_POSIX)
#include <fcntl.h>

#include "base/files/file_descriptor_watcher_posix.h"
#endif
 ...
```
### patch
```
#include "brave/base/test/launcher/teamcity_reporter.h"

```

### match
```
...
#include "base/path_service.h"

 #endif 
 >>> 
 ...
```
### patch
```
#define TestLauncher TestLauncher_ChromiumImpl


```

### match
```
...   >>> 
 results_tracker_.AddTestResult(result);  <<< ...
```
### patch
```
    results_tracker_.AddTestResult(OnTestResult(result));

```

### match
```
...
std::string TruncateSnippetFocused(std::string_view snippet,
                                   size_t byte_limit) {
  // Find the start of anything that looks like a fatal log message.
  // We want to preferentially preserve these from truncation as we
  // run extraction of fatal test errors from snippets in result_adapter
  // to populate failure reasons in ResultDB. It is also convenient for
  // the user to see them.
  // Refer to LogMessage::Init in base/logging[_platform].cc for patterns.
  size_t fatal_message_pos =
      std::min(snippet.find("FATAL:"), snippet.find("FATAL "));

  size_t fatal_message_start = 0;
  size_t fatal_message_end = 0;
  if (fatal_message_pos != std::string::npos) {
    // Find the line-endings before and after the fatal message.
    size_t start_pos = snippet.rfind("\n", fatal_message_pos);
    if (start_pos != std::string::npos) {
      fatal_message_start = start_pos;
    }
    size_t end_pos = snippet.find("\n", fatal_message_pos);
    if (end_pos != std::string::npos) {
      // Include the new-line character.
      fatal_message_end = end_pos + 1;
    } else {
      fatal_message_end = snippet.length();
    }
  }
  // Limit fatal message length to half the snippet byte quota. This ensures
  // we have space for some context at the beginning and end of the snippet.
  fatal_message_end =
      std::min(fatal_message_end, fatal_message_start + (byte_limit / 2));

  // Distribute remaining bytes between start and end of snippet.
  // The split is either even, or if one is small enough to be displayed
  // without truncation, it gets displayed in full and the other split gets
  // the remaining bytes.
  size_t remaining_bytes =
      byte_limit - (fatal_message_end - fatal_message_start);
  size_t start_split_bytes;
  size_t end_split_bytes;
  if (fatal_message_start < remaining_bytes / 2) {
    start_split_bytes = fatal_message_start;
    end_split_bytes = remaining_bytes - fatal_message_start;
  } else if ((snippet.length() - fatal_message_end) < remaining_bytes / 2) {
    start_split_bytes =
        remaining_bytes - (snippet.length() - fatal_message_end);
    end_split_bytes = (snippet.length() - fatal_message_end);
  } else {
    start_split_bytes = remaining_bytes / 2;
    end_split_bytes = remaining_bytes - start_split_bytes;
  }
  return base::StrCat(
      {TruncateSnippet(snippet.substr(0, fatal_message_start),
                       start_split_bytes),
       snippet.substr(fatal_message_start,
                      fatal_message_end - fatal_message_start),
       TruncateSnippet(snippet.substr(fatal_message_end), end_split_bytes)});
}
 >>> 
...
```
### patch
```
TestLauncher::TestLauncher(TestLauncherDelegate* launcher_delegate,
                           size_t parallel_jobs,
                           size_t retry_limit)
    : TestLauncher_ChromiumImpl(launcher_delegate, parallel_jobs, retry_limit) {
  teamcity_reporter_ = TeamcityReporter::MaybeCreate();
}

TestLauncher::~TestLauncher() = default;

void TestLauncher::OnTestFinished(const TestResult& result) {
  // The order of TC log calls is important here. First we want to let TC know a
  // test is starting, then we call the original `OnTestFinished` which may
  // print the test output on failure, so it will become a part of the
  // TC-reported test. Finally we want to let TC know the test is finished so
  // any other test launcher output should not be bound to the test.
  if (teamcity_reporter_) {
    teamcity_reporter_->OnTestStarted(result);
  }

  // Upstream implementation of this method does roughly this:
  // 1. Print the test output if it has failed.
  // 2. Add test results via `results_tracker_.AddTestResult()`.
  // 3. Call exit(1) if a lot of test have failed.
  //
  // TestLauncher::OnTestResult() will be called from AddTestResult() override.
  // TestLauncher::MaybeSaveSummaryAsJSON() will be called before exit(1).
  TestLauncher_ChromiumImpl::OnTestFinished(result);

  if (teamcity_reporter_) {
    teamcity_reporter_->OnTestFinished(result);
  }
}

void TestLauncher::CreateAndStartThreadPool(size_t num_parallel_jobs) {
  // `retry_limit_` can be overridden by command line. Read its value when all
  // command line flags are parsed.
  if (teamcity_reporter_) {
    teamcity_reporter_->SetRetryLimit(retry_limit_);
  }

  TestLauncher_ChromiumImpl::CreateAndStartThreadPool(num_parallel_jobs);
}

// This is called from TestLauncher_ChromiumImpl::OnTestFinished() via
// AddTestResult() override.
const TestResult& TestLauncher::OnTestResult(const TestResult& result) {
  if (teamcity_reporter_) {
    teamcity_reporter_->OnTestResult(result);
  }
  return result;
}

void TestLauncher::MaybeSaveSummaryAsJSON(
    const std::vector<std::string>& additional_tags) {
  // This may be called from TestLauncher_ChromiumImpl::OnTestFinished() when a
  // lot of test has failed and the TestLauncher decides to do an early exit.
  if (teamcity_reporter_ &&
      std::ranges::contains(additional_tags, "BROKEN_TEST_EARLY_EXIT")) {
    // TestLauncher will call exit(1) before returning from OnTestFinished(), so
    // log the test suite shutdown here while we can.
    teamcity_reporter_->OnBrokenTestEarlyExit();
  }

  TestLauncher_ChromiumImpl::MaybeSaveSummaryAsJSON(additional_tags);
}


```

