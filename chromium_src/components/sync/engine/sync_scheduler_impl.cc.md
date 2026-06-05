### match
```cpp
...
#include <cstring>

 #include <utility>
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```cpp
#include "base/functional/callback_forward.h"
#include "base/logging.h"
#include "brave/components/sync/engine/brave_sync_server_commands.h"
#include "base/functional/callback.h"
#include "components/sync/engine/sync_protocol_error.h"

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 void SyncSchedulerImpl::HandleFailure(
    const ModelNeutralState& model_neutral_state) { ... 
 
 else { ... 
SDVLOG(2) << "Sync cycle failed.  Will back off for "
              << wait_interval_->length.InMilliseconds() << "ms.";
 } 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  HandleBraveConfigurationFailure(model_neutral_state);

```

### match
```cpp
...
 
 namespace syncer { ... 
bool SyncSchedulerImpl::IsEarlierThanCurrentPendingJob(
    const base::TimeDelta& delay) {
  TimeTicks incoming_run_time = TimeTicks::Now() + delay;
  if (pending_wakeup_timer_.IsRunning() &&
      (pending_wakeup_timer_.desired_run_time() < incoming_run_time)) {
    // Old job arrives sooner than this one.
    return false;
  }
  return true;
}
 #undef SDVLOG
 
 >>> 
 ... } ...  
```
### patch
```cpp
void SyncSchedulerImpl::HandleBraveConfigurationFailure(
    const ModelNeutralState& model_neutral_state) {
  if (model_neutral_state.last_server_error_message ==
      kNigoriFolderNotReadyError) {
    VLOG(1) << "Got nigori root folder error from sync server. Override wait "
               "interval to 3 sec";
    wait_interval_.emplace(WaitInterval::BlockingMode::kThrottled,
                           base::Seconds(3));
  }
}
void SyncSchedulerImpl::SchedulePermanentlyDeleteAccount(
    base::OnceCallback<void(const SyncProtocolError&)> callback) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);

  base::SequencedTaskRunner::GetCurrentDefault()->PostTask(
      FROM_HERE,
      base::BindOnce(&SyncSchedulerImpl::PermanentlyDeleteAccountImpl,
                     weak_ptr_factory_.GetWeakPtr(), std::move(callback)));
}

void SyncSchedulerImpl::PermanentlyDeleteAccountImpl(
    base::OnceCallback<void(const SyncProtocolError&)> callback) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);

  SyncCycle cycle(cycle_context_, this);
  BraveSyncServerCommands::PermanentlyDeleteAccount(&cycle,
                                                    std::move(callback));
}

```

