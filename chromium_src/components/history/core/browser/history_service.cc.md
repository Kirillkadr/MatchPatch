### match
```cpp
...
void HistoryService::LogTransitionMetricsForVisit(
    ui::PageTransition transition) {
  // A generic measure of whether the visits are coming from the main frame or a
  // subframe.
  base::UmaHistogramBoolean("History.VisitedLinks.VisitLoggedFromMainFrame",
                            ui::PageTransitionIsMainFrame(transition));
  // A metric which records whether a visit matches one of the
  // ui::PageTransition types of interest: link, typed, or manual subframe.
  // Otherwise, it is recorded as "other".
  switch (ui::PageTransitionStripQualifier(transition)) {
    case ui::PageTransition::PAGE_TRANSITION_LINK:
      base::UmaHistogramEnumeration(
          "History.VisitedLinks.VisitLoggedFromTransition",
          PageTransitionForVisitedLinks::kLink);
      break;
    case ui::PageTransition::PAGE_TRANSITION_TYPED:
      base::UmaHistogramEnumeration(
          "History.VisitedLinks.VisitLoggedFromTransition",
          PageTransitionForVisitedLinks::kTyped);
      break;
    case ui::PageTransition::PAGE_TRANSITION_MANUAL_SUBFRAME:
      base::UmaHistogramEnumeration(
          "History.VisitedLinks.VisitLoggedFromTransition",
          PageTransitionForVisitedLinks::kManualSubframe);
      break;
    default:
      base::UmaHistogramEnumeration(
          "History.VisitedLinks.VisitLoggedFromTransition",
          PageTransitionForVisitedLinks::kOther);
  }
}
 >>> 
 ...
```
### patch
```cpp
void HistoryService::GetKnownToSyncCount(
    base::OnceCallback<void(HistoryCountResult)> callback) {
  backend_task_runner_->PostTaskAndReplyWithResult(
      FROM_HERE,
      base::BindOnce(&HistoryBackend::GetKnownToSyncCount, history_backend_),
      std::move(callback));
}

```

