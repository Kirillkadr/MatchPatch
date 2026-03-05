### match
```
...
#include "ui/accessibility/accessibility_features.h"

 #include "ui/display/screen_info.h"
 
 >>> 
#ifndef LOG_MEDIA_EVENTS
// Default to not logging events because so many are generated they can
// overwhelm the rest of the logging.
#define LOG_MEDIA_EVENTS 0
#endif
 ...
```
### patch
```
#include "third_party/blink/renderer/core/html/media/autoplay_policy.h"

```

### match
```
...
#define LOG_OFFICIAL_TIME_STATUS 0

 #endif 
 >>> 
 ...
```
### patch
```
bool SkipPauseIfAutoplayIsBlockedByPolicy(bool is_gesture_needed) {
  if (is_gesture_needed)
    return false;
  return true;
}

```

### match
```
...   >>> 
 if(EffectiveMediaVolume() && !autoplay_policy_->RequestAutoplayUnmute())  <<< pause();
// If playback was not paused by the autoplay policy and got audible, the
  // element is marked as being allowed to play unmuted.
  if (EffectiveMediaVolume() && PotentiallyPlaying())
    was_always_muted_ = false;

  if (web_media_player_)
    web_media_player_->SetVolume(EffectiveMediaVolume());
 ...
```
### patch
```
  if (EffectiveMediaVolume() && !autoplay_policy_->RequestAutoplayUnmute() &&
      SkipPauseIfAutoplayIsBlockedByPolicy(
          autoplay_policy_->IsGestureNeededForPlayback()) &&
      EffectiveMediaVolume())

```

### match
```
...   >>> 
 if 
 (EffectiveMediaVolume() && !autoplay_policy_->RequestAutoplayUnmute())  <<< ... 
pause();
 
  // If playback was not paused by the autoplay policy and got unmuted, the
  // element is marked as being allowed to play unmuted.
  if (EffectiveMediaVolume() && PotentiallyPlaying())
    was_always_muted_ = false;

  // This is called at the end to make sure the WebMediaPlayer has the right
  // information.
  if (web_media_player_)
    web_media_player_->SetVolume(EffectiveMediaVolume());

  autoplay_policy_->StopAutoplayMutedWhenVisible();
}

void HTMLMediaElement::SetUserWantsControlsVisible(bool visible) {
  user_wants_controls_visible_ = visible;
  UpdateControlsVisibility();
} ...
```
### patch
```
  if (EffectiveMediaVolume() && !autoplay_policy_->RequestAutoplayUnmute() &&
      SkipPauseIfAutoplayIsBlockedByPolicy(
          autoplay_policy_->IsGestureNeededForPlayback()) &&
      EffectiveMediaVolume())

```

