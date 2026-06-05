### match
```cpp
...
 
 namespace syncer { ... 
 
 TEST_F(SyncSchedulerImplTest, InterleavedNudgesStillRestart) { ... 
EXPECT_TRUE(scheduler()->IsGlobalBackoff());
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
namespace {
void SimulatePollFailedRegularTransientError(DataTypeSet requested_types,
                                             SyncCycle* cycle) {
  cycle->mutable_status_controller()->set_last_download_updates_result(
      SyncerError::ProtocolError(TRANSIENT_ERROR));
}

void SimulatePollFailedNigoryNotReady(DataTypeSet requested_types,
                                      SyncCycle* cycle) {
  cycle->mutable_status_controller()->set_last_download_updates_result(
      SyncerError::ProtocolError(TRANSIENT_ERROR));

  cycle->mutable_status_controller()->set_last_server_error_message(
      kNigoriFolderNotReadyError);
}

}  // namespace

TEST_F(SyncSchedulerImplTest, BraveNoBackoffOnNigoriError) {
  scheduler()->OnReceivedPollIntervalUpdate(base::Milliseconds(10));
  UseMockDelayProvider();  // Will cause test failure if backoff is initiated.
  EXPECT_CALL(*delay(), GetDelay).WillRepeatedly(Return(base::Milliseconds(0)));

  SyncShareTimes times;
  EXPECT_CALL(*syncer(), PollSyncShare)
      .WillOnce(DoAll(SimulatePollFailedNigoryNotReady,
                      RecordSyncShare(&times, false)))
      .WillOnce(DoAll(SimulatePollFailedRegularTransientError,
                      RecordSyncShare(&times, false)));

  StartSyncScheduler(base::Time());

  // Nigory folder error should not trigger backoff.
  RunLoop();
  EXPECT_FALSE(scheduler()->IsGlobalBackoff());

  // Regular transient error should trigger backoff.
  RunLoop();
  EXPECT_TRUE(scheduler()->IsGlobalBackoff());
}

```

