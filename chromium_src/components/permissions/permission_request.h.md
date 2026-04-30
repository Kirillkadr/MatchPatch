### match
```cpp
...
 
 # ifndef ... 
#include <string>

 #include <variant>
 
 >>> 
#include "base/functional/callback.h"

 ... 
```
### patch
```cpp
#include <optional>
#include "components/permissions/permission_hats_trigger_helper.h"
#include "base/memory/weak_ptr.h"
#include "base/time/time.h"

```

### match
```cpp
...
 
 # ifndef ... 
 namespace 
 permissions 
 { 
 >>> 
enum class RequestType
 ... } ...  
```
### patch
```cpp
class PermissionRequest : public PermissionRequest_ChromiumImpl {
 public:
  PermissionRequest(
      std::unique_ptr<PermissionRequestData> request_data,
      PermissionDecidedCallback permission_decided_callback,
      base::OnceClosure request_finished_callback = base::DoNothing(),
      bool uses_automatic_embargo = true);

  PermissionRequest(const PermissionRequest&) = delete;
  PermissionRequest& operator=(const PermissionRequest&) = delete;

  ~PermissionRequest() override;

#if BUILDFLAG(IS_ANDROID)
  AnnotatedMessageText GetDialogAnnotatedMessageText(
      const GURL& embedding_origin) const override;

  static AnnotatedMessageText GetDialogAnnotatedMessageText(
      std::u16string requesting_origin_formatted_for_display,
      int message_id,
      bool format_origin_bold);
#endif

  bool SupportsLifetime() const;
  void SetLifetime(std::optional<base::TimeDelta> lifetime);
  const std::optional<base::TimeDelta>& GetLifetime() const;

  void set_dont_ask_again(bool dont_ask_again) {
    dont_ask_again_ = dont_ask_again;
  }
  bool get_dont_ask_again() const { return dont_ask_again_; }

  // We rename upstream's IsDuplicateOf() via a define above and re-declare it
  // here to workaround the fact that the PermissionRequest_ChromiumImpl rename
  // will affect this method's only parameter too, which will break subclasses.
  virtual bool IsDuplicateOf(PermissionRequest* other_request) const;

  // Returns a weak pointer to this instance.
  base::WeakPtr<PermissionRequest> GetWeakPtr();

 private:
  std::optional<base::TimeDelta> lifetime_;

  bool dont_ask_again_ = false;

  base::WeakPtrFactory<PermissionRequest> weak_factory_{this};
};

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ...   >>> 
 class 
 PermissionRequest 
 {  <<< 
public
 ... } ...  } ...  
```
### patch
```cpp
class PermissionRequest_ChromiumImpl {

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
// need to be shown in the UI.  >>> 
 virtual bool IsDuplicateOf(PermissionRequest* other_request) const;  <<< 
#if BUILDFLAG(IS_ANDROID) || BUILDFLAG(IS_IOS)
  // A message text with formatting information.
  struct AnnotatedMessageText {
    // |text| specifies the text string itself.
    // |bolded_ranges| defines a (potentially empty) list of ranges represented
    // as pairs of <textOffset, rangeSize>, which shall be used by the UI to
    // format the specified ranges as bold text.
    AnnotatedMessageText(std::u16string text,
                         std::vector<std::pair<size_t, size_t>> bolded_ranges);
    ~AnnotatedMessageText();
    AnnotatedMessageText(const AnnotatedMessageText& other) = delete;
    AnnotatedMessageText& operator=(const AnnotatedMessageText& other) = delete;

    std::u16string text;

    // A list of ranges defined as pairs of <offset, size> which
    // will be used by Clank to format the ranges in |text| as bold.
    std::vector<std::pair<size_t, size_t>> bolded_ranges;
  };

  virtual AnnotatedMessageText GetDialogAnnotatedMessageText(
      const GURL& embedding_origin) const;

  // Returns prompt text appropriate for displaying in an Android dialog.
  static AnnotatedMessageText GetDialogAnnotatedMessageText(
      std::u16string requesting_origin_formatted_for_display,
      int message_id,
      bool format_origin_bold);
#endif
 ... } ...  
```
### patch
```cpp
  virtual bool IsDuplicateOf_ChromiumImpl(PermissionRequest* other_request) const;

```

