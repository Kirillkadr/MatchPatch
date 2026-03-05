### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::MessageDataDeleter::MessageDataDeleter 
 (  <<< ... 
v8::Isolate* isolate
 ... ) ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::MessageDataDeleter::MessageDataDeleter(

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::MessageDataDeleter::operator()(uint8_t* p) const 
 {  <<< ... 
DCHECK(isolate_) << "Cannot call deleter when default constructor was used";
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::MessageDataDeleter::operator()(uint8_t* p) const {

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::MessageData 
 WebSocketChannelImpl::CreateMessageData 
 (  <<< ... 
v8::Isolate* isolate
 ... ) ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::MessageData WebSocketChannelImpl_ChromiumImpl::CreateMessageData(

```

### match
```
...
 namespace blink { ...   >>> 
 class 
 WebSocketChannelImpl::BlobLoader 
 final 
 : 
 public 
 GarbageCollected<WebSocketChannelImpl::BlobLoader> 
 ,  <<< ... 
public
 ... } ...  
```
### patch
```
class WebSocketChannelImpl_ChromiumImpl::BlobLoader final
    : public GarbageCollected<WebSocketChannelImpl_ChromiumImpl::BlobLoader>,

```

### match
```
...
 namespace blink { ... 
 class WebSocketChannelImpl_ChromiumImpl::BlobLoader final
	    : public GarbageCollected<WebSocketChannelImpl_ChromiumImpl::BlobLoader>,
	public FileReaderClient { ...   >>> 
 WebSocketChannelImpl* 
 ,  <<< ... 
scoped_refptr<base::SingleThreadTaskRunner>
 ... } ...  } ...  
```
### patch
```
             WebSocketChannelImpl_ChromiumImpl*,

```

### match
```
...
 namespace blink { ...   >>> 
 Member<WebSocketChannelImpl> channel_;  <<< ... 
Member<FileReaderLoader> loader_;
 ... } ...  
```
### patch
```
  Member<WebSocketChannelImpl_ChromiumImpl> channel_;

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::BlobLoader::BlobLoader 
 (  <<< ... 
scoped_refptr<BlobDataHandle> blob_data_handle
 ... ) ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::BlobLoader::BlobLoader(

```

### match
```
...
 namespace blink { ... 
 WebSocketChannelImpl_ChromiumImpl::BlobLoader::BlobLoader ( ...   >>> 
 WebSocketChannelImpl* channel 
 ,  <<< ... 
scoped_refptr<base::SingleThreadTaskRunner> task_runner
 ... ) ...  } ...  
```
### patch
```
    WebSocketChannelImpl_ChromiumImpl* channel,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::BlobLoader::Cancel() 
 {  <<< ... 
loader_->Cancel();
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::BlobLoader::Cancel() {

```

### match
```
...
 namespace blink { ...   >>> 
 FileErrorCode 
 WebSocketChannelImpl::BlobLoader::DidStartLoading(uint64_t) 
 {  <<< ... 
const std::optional<uint64_t> size = loader_->TotalBytes();
 ... } ...  } ...  
```
### patch
```
FileErrorCode WebSocketChannelImpl_ChromiumImpl::BlobLoader::DidStartLoading(uint64_t) {

```

### match
```
...
>>>
 data_ 
 = 
 WebSocketChannelImpl::CreateMessageData 
 (  <<< ... 
channel_->execution_context_->GetIsolate()
 ... ) ...  
```
### patch
```
  data_ = WebSocketChannelImpl_ChromiumImpl::CreateMessageData(

```

### match
```
...
 namespace blink { ...   >>> 
 FileErrorCode 
 WebSocketChannelImpl::BlobLoader::DidReceiveData 
 (  <<< ... 
base::span<const uint8_t> data
 ... ) ...  } ...  
```
### patch
```
FileErrorCode WebSocketChannelImpl_ChromiumImpl::BlobLoader::DidReceiveData(

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::BlobLoader::DidFinishLoading() 
 {  <<< ... 
// This is guaranteed by FileReaderLoader::OnDataPipeReadable.
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::BlobLoader::DidFinishLoading() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::BlobLoader::DidFail(FileErrorCode error_code) 
 {  <<< ... 
if (error_code == FileErrorCode::kAbortErr && blob_too_large_) {
    blob_too_large_ = false;
    channel_->BlobTooLarge();
  }
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::BlobLoader::DidFail(FileErrorCode error_code) {

```

### match
```
...
 namespace blink { ...   >>> 
 struct 
 WebSocketChannelImpl::ConnectInfo 
 {  <<< ... 
ConnectInfo(const String& selected_protocol, const String& extensions)
      : selected_protocol(selected_protocol), extensions(extensions) {}
 ... } ...  } ...  
```
### patch
```
struct WebSocketChannelImpl_ChromiumImpl::ConnectInfo {

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl 
 * 
 WebSocketChannelImpl::CreateForTesting 
 (  <<< ... 
ExecutionContext* execution_context
 ... ) ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl* WebSocketChannelImpl_ChromiumImpl::CreateForTesting(

```

### match
```
...
 namespace blink { ... 
 WebSocketChannelImpl_ChromiumImpl* WebSocketChannelImpl_ChromiumImpl::CreateForTesting(
	ExecutionContext* execution_context,
    WebSocketChannelClient* client,
    SourceLocation* location,
    std::unique_ptr<WebSocketHandshakeThrottle> handshake_throttle) { ...   >>> 
 auto 
 * channel 
 = 
 MakeGarbageCollected<WebSocketChannelImpl> 
 (  <<< ... ) ...  } ...  } ...  
```
### patch
```
  auto* channel = MakeGarbageCollected<WebSocketChannelImpl_ChromiumImpl>(

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl 
 * 
 WebSocketChannelImpl::Create 
 (  <<< ... 
ExecutionContext* execution_context
 ... ) ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl* WebSocketChannelImpl_ChromiumImpl::Create(

```

### match
```
...
 namespace blink { ... 
 WebSocketChannelImpl_ChromiumImpl* WebSocketChannelImpl_ChromiumImpl::Create(
	ExecutionContext* execution_context,
    WebSocketChannelClient* client,
    SourceLocation* location) { ...   >>> 
 auto 
 * channel 
 = 
 MakeGarbageCollected<WebSocketChannelImpl> 
 (  <<< ... ) ...  } ...  } ...  
```
### patch
```
  auto* channel = MakeGarbageCollected<WebSocketChannelImpl_ChromiumImpl>(

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::WebSocketChannelImpl 
 ( 
 ExecutionContext* execution_context 
 ,  <<< ... 
WebSocketChannelClient* client
 ... ) ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::WebSocketChannelImpl_ChromiumImpl(ExecutionContext* execution_context,

```

### match
```
...
 namespace blink { ... 
WebSocketChannelImpl_ChromiumImpl::WebSocketChannelImpl_ChromiumImpl(ExecutionContext* execution_context,
	WebSocketChannelClient* client,
                                           SourceLocation* location)
    : client_(client),
      identifier_(CreateUniqueIdentifier()),
      message_chunks_(MakeGarbageCollected<WebSocketMessageChunkAccumulator>(
          execution_context->GetTaskRunner(TaskType::kNetworking))),
      execution_context_(execution_context),
      location_at_construction_(location),
      websocket_(execution_context),
      handshake_client_receiver_(this, execution_context),
      client_receiver_(this, execution_context),
      readable_watcher_(
          FROM_HERE,
          mojo::SimpleWatcher::ArmingPolicy::MANUAL,
          execution_context->GetTaskRunner(TaskType::kNetworking)),
      writable_watcher_(
          FROM_HERE,
          mojo::SimpleWatcher::ArmingPolicy::MANUAL,
          execution_context->GetTaskRunner(TaskType::kNetworking)),
      file_reading_task_runner_(
          execution_context->GetTaskRunner(TaskType::kFileReading)) {}  >>> 
 WebSocketChannelImpl::~WebSocketChannelImpl() = default;  <<< ... 
bool WebSocketChannelImpl::Connect(const KURL& url, const String& protocol) {
  DVLOG(1) << this << " Connect()";

  if (GetBaseFetchContext()->ShouldBlockWebSocketByMixedContentCheck(url)) {
    has_initiated_opening_handshake_ = false;
    return false;
  }

  if (auto* scheduler = execution_context_->GetScheduler()) {
    // Two features are registered here:
    // - `kWebSocket`: a non-sticky feature that will disable BFCache for any
    // page. It will be reset after the `WebSocketChannel` is closed.
    // - `kWebSocketSticky`: a sticky feature that will only disable BFCache for
    // the page containing "Cache-Control: no-store" header. It won't be reset
    // even if the `WebSocketChannel` is closed.
    feature_handle_for_scheduler_ = scheduler->RegisterFeature(
        SchedulingPolicy::Feature::kWebSocket,
        SchedulingPolicy{SchedulingPolicy::DisableBackForwardCache()});
    scheduler->RegisterStickyFeature(
        SchedulingPolicy::Feature::kWebSocketSticky,
        SchedulingPolicy{SchedulingPolicy::DisableBackForwardCache()});
  }

  if (MixedContentChecker::IsMixedContent(
          execution_context_->GetSecurityOrigin(), url)) {
    String message =
        "Connecting to a non-secure WebSocket server from a secure origin is "
        "deprecated.";
    execution_context_->AddConsoleMessage(MakeGarbageCollected<ConsoleMessage>(
        mojom::blink::ConsoleMessageSource::kJavaScript,
        mojom::blink::ConsoleMessageLevel::kWarning, message));
  }

  url_ = url;
  Vector<String> protocols;
  // Avoid placing an empty token in the Vector when the protocol string is
  // empty.
  if (!protocol.empty()) {
    // Since protocol is already verified and escaped, we can simply split
    // it.
    protocols = protocol.Split(", ");
  }

  // If the connection needs to be filtered, asynchronously fail. Synchronous
  // failure blocks the worker thread which should be avoided. Note that
  // returning "true" just indicates that this was not a mixed content error.
  if (ShouldDisallowConnection(url)) {
    execution_context_->GetTaskRunner(TaskType::kNetworking)
        ->PostTask(FROM_HERE,
                   BindOnce(&WebSocketChannelImpl::TearDownFailedConnection,
                            WrapPersistent(this)));
    return true;
  }

  // Restrict the number of simultaneous connections to avoid a DoS attack on
  // the browser process. Fail asynchronously, to match the behaviour when we
  // are throttled by the network service.
  if (connection_count_tracker_handle_.IncrementAndCheckStatus() ==
      ConnectionCountTrackerHandle::CountStatus::kShouldNotConnect) {
    StringBuilder message;
    message.Append("WebSocket connection to '");
    message.Append(url.GetString());
    message.Append("' failed: Insufficient resources");
    execution_context_->AddConsoleMessage(MakeGarbageCollected<ConsoleMessage>(
        mojom::blink::ConsoleMessageSource::kNetwork,
        mojom::blink::ConsoleMessageLevel::kError, message.ToString()));
    execution_context_->GetTaskRunner(TaskType::kNetworking)
        ->PostTask(FROM_HERE,
                   BindOnce(&WebSocketChannelImpl::TearDownFailedConnection,
                            WrapPersistent(this)));
    return true;
  }

  mojo::Remote<mojom::blink::WebSocketConnector> connector;
  execution_context_->GetBrowserInterfaceBroker().GetInterface(
      connector.BindNewPipeAndPassReceiver(
          execution_context_->GetTaskRunner(TaskType::kWebSocket)));

  std::optional<base::UnguessableToken> devtools_token;
  probe::WillCreateWebSocket(execution_context_, identifier_, url, protocol,
                             &devtools_token);

  connector->Connect(
      url, protocols, execution_context_->UserAgent(),
      execution_context_->GetStorageAccessApiStatus(),
      handshake_client_receiver_.BindNewPipeAndPassRemote(
          execution_context_->GetTaskRunner(TaskType::kWebSocket)),
      /*throttling_profile_id=*/devtools_token);
  handshake_client_receiver_.set_disconnect_with_reason_handler(
      blink::BindOnce(&WebSocketChannelImpl::OnConnectionError,
                      WrapWeakPersistent(this), FROM_HERE));
  has_initiated_opening_handshake_ = true;

  if (handshake_throttle_) {
    scoped_refptr<const SecurityOrigin> isolated_security_origin;
    const DOMWrapperWorld* world = execution_context_->GetCurrentWorld();
    // TODO(crbug.com/40511450): Current world can be null because of PPAPI.
    // Null check can be cleaned up once PPAPI support is removed.
    if (world && world->IsIsolatedWorld()) {
      isolated_security_origin = world->IsolatedWorldSecurityOrigin(
          execution_context_->GetAgentClusterID());
    }
    // The use of WrapWeakPersistent is safe and motivated by the fact that if
    // the WebSocket is no longer referenced, there's no point in keeping it
    // alive just to receive the throttling result.
    handshake_throttle_->ThrottleHandshake(
        url, WebSecurityOrigin(execution_context_->GetSecurityOrigin()),
        isolated_security_origin ? WebSecurityOrigin(isolated_security_origin)
                                 : WebSecurityOrigin(),
        BindOnce(&WebSocketChannelImpl::OnCompletion,
                 WrapWeakPersistent(this)));
  } else {
    // Treat no throttle as success.
    throttle_passed_ = true;
  }

  DEVTOOLS_TIMELINE_TRACE_EVENT_INSTANT(
      "WebSocketCreate", InspectorWebSocketCreateEvent::Data,
      execution_context_.Get(), identifier_, url, protocol);
  return true;
}
 ... } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::~WebSocketChannelImpl_ChromiumImpl() = default;

```

### match
```
...
 namespace blink { ...   >>> 
 bool 
 WebSocketChannelImpl::Connect(const KURL& url, const String& protocol) 
 {  <<< ... 
DVLOG(1) << this << " Connect()";
 ... } ...  } ...  
```
### patch
```

bool WebSocketChannelImpl_ChromiumImpl::Connect(const KURL& url, const String& protocol) {

```

### match
```
...
 if (ShouldDisallowConnection(url)) { ...   >>> 
 BindOnce 
 ( 
 &WebSocketChannelImpl::TearDownFailedConnection 
 ,  <<< ... 
WrapPersistent(this)
 ... ) ...  } ...  
```
### patch
```
                   BindOnce(&WebSocketChannelImpl_ChromiumImpl::TearDownFailedConnection,

```

### match
```
...
 if (connection_count_tracker_handle_.IncrementAndCheckStatus() ==
      ConnectionCountTrackerHandle::CountStatus::kShouldNotConnect) { ...   >>> 
 BindOnce 
 ( 
 &WebSocketChannelImpl::TearDownFailedConnection 
 ,  <<< ... 
WrapPersistent(this)
 ... ) ...  } ...  
```
### patch
```
                   BindOnce(&WebSocketChannelImpl_ChromiumImpl::TearDownFailedConnection,

```

### match
```
...
 namespace blink { ... 
 handshake_client_receiver_.set_disconnect_with_reason_handler ( ...   >>> 
 blink::BindOnce 
 ( 
 &WebSocketChannelImpl::OnConnectionError 
 ,  <<< ... 
WrapWeakPersistent(this)
 ... ) ...  ) ...  } ...  
```
### patch
```
      blink::BindOnce(&WebSocketChannelImpl_ChromiumImpl::OnConnectionError,

```

### match
```
...
 if (handshake_throttle_) { ...   >>> 
 BindOnce 
 ( 
 &WebSocketChannelImpl::OnCompletion 
 ,  <<< ... 
WrapWeakPersistent(this)
 ... ) ...  } ...  
```
### patch
```
        BindOnce(&WebSocketChannelImpl_ChromiumImpl::OnCompletion,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::Send 
 (  <<< ... 
const std::string& message
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::Send(

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::Send 
 (  <<< ... 
scoped_refptr<BlobDataHandle> blob_data_handle
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::Send(

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::Send 
 (  <<< ... 
const DOMArrayBuffer& buffer
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::Send(

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::Close(int code, const String& reason) 
 {  <<< ... 
DCHECK_EQ(GetState(), State::kOpen);
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::Close(int code, const String& reason) {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::Fail 
 ( 
 const String& reason 
 ,  <<< ... 
mojom::ConsoleMessageLevel level
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::Fail(const String& reason,

```

### match
```
...
>>>
 BindOnce 
 ( 
 &WebSocketChannelImpl::TearDownFailedConnection 
 ,  <<< ... 
WrapPersistent(this)
 ... ) ...  
```
### patch
```
                 BindOnce(&WebSocketChannelImpl_ChromiumImpl::TearDownFailedConnection,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::Disconnect() 
 {  <<< ... 
DVLOG(1) << this << " Disconnect()";
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::Disconnect() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::CancelHandshake() 
 {  <<< ... 
DVLOG(1) << this << " CancelHandshake()";
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::CancelHandshake() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::ApplyBackpressure() 
 {  <<< ... 
DVLOG(1) << this << " ApplyBackpressure";
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::ApplyBackpressure() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::RemoveBackpressure() 
 {  <<< ... 
DVLOG(1) << this << " RemoveBackpressure";
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::RemoveBackpressure() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::OnOpeningHandshakeStarted 
 (  <<< ... 
network::mojom::blink::WebSocketHandshakeRequestPtr request
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::OnOpeningHandshakeStarted(

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::OnFailure 
 ( 
 const String& message 
 ,  <<< ... 
int net_error
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::OnFailure(const String& message,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::OnConnectionEstablished 
 (  <<< ... 
mojo::PendingRemote<network::mojom::blink::WebSocket> websocket
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::OnConnectionEstablished(

```

### match
```
...
 namespace blink { ... 
 client_receiver_.set_disconnect_with_reason_handler ( ...   >>> 
 blink::BindOnce 
 ( 
 &WebSocketChannelImpl::OnConnectionError 
 ,  <<< ... 
WrapWeakPersistent(this)
 ... ) ...  ) ...  } ...  
```
### patch
```
      blink::BindOnce(&WebSocketChannelImpl_ChromiumImpl::OnConnectionError,

```

### match
```
...
>>>
 BindRepeating 
 ( 
 &WebSocketChannelImpl::OnReadable 
 ,  <<< ... 
WrapWeakPersistent(this)
 ... ) ...  
```
### patch
```
                              BindRepeating(&WebSocketChannelImpl_ChromiumImpl::OnReadable,

```

### match
```
...
>>>
 BindRepeating 
 ( 
 &WebSocketChannelImpl::OnWritable 
 ,  <<< ... 
WrapWeakPersistent(this)
 ... ) ...  
```
### patch
```
                              BindRepeating(&WebSocketChannelImpl_ChromiumImpl::OnWritable,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::OnDataFrame 
 ( 
 bool fin 
 ,  <<< ... 
MessageTypeForMojo type
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::OnDataFrame(bool fin,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::OnDropChannel 
 ( 
 bool was_clean 
 ,  <<< ... 
uint16_t code
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::OnDropChannel(bool was_clean,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::OnClosingHandshake() 
 {  <<< ... 
DCHECK_EQ(GetState(), State::kOpen);
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::OnClosingHandshake() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::Trace(Visitor* visitor) const 
 {  <<< ... 
visitor->Trace(blob_loader_);
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::Trace(Visitor* visitor) const {

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::Message::Message 
 (  <<< ... 
scoped_refptr<BlobDataHandle> blob_data_handle
 ... ) ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::Message::Message(

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::Message::Message(MessageData data)  <<< ... 
: message_data_(std::move(data)),
      type_(kMessageTypeArrayBuffer),
      pending_payload_(message_data_.as_span())
 ... } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::Message::Message(MessageData data)

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::Message::Message 
 (  <<< ... 
MessageType type
 ... ) ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::Message::Message(

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::Message::Message(uint16_t code, const String& reason)  <<< ... 
: type_(kMessageTypeClose), code_(code), reason_(reason)
 ... } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::Message::Message(uint16_t code, const String& reason)

```

### match
```
...
 namespace blink { ... 
WebSocketChannelImpl_ChromiumImpl::Message::Message(uint16_t code, const String& reason)
	: type_(kMessageTypeClose), code_(code), reason_(reason) {}  >>> 
 WebSocketChannelImpl::Message::Message(Message&&) = default;  <<< ... 
WebSocketChannelImpl::Message& WebSocketChannelImpl::Message::operator=(
    Message&&) = default;
 ... } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::Message::Message(Message&&) = default;

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::Message 
 & 
 WebSocketChannelImpl::Message::operator= 
 (  <<< ... 
Message&&
 ... ) ...  } ...  
```
### patch
```

WebSocketChannelImpl_ChromiumImpl::Message& WebSocketChannelImpl_ChromiumImpl::Message::operator=(

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::State 
 WebSocketChannelImpl::GetState() const 
 {  <<< ... 
if (!has_initiated_opening_handshake_) {
    return State::kConnecting;
  }
 ... } ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::State WebSocketChannelImpl_ChromiumImpl::GetState() const {

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::MessageType 
 WebSocketChannelImpl::Message::Type() const 
 {  <<< ... 
return type_;
 ... } ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::MessageType WebSocketChannelImpl_ChromiumImpl::Message::Type() const {

```

### match
```
...
 namespace blink { ... 
scoped_refptr<BlobDataHandle>  >>> 
 WebSocketChannelImpl::Message::GetBlobDataHandle() 
 {  <<< ... 
return blob_data_handle_;
 ... } ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::Message::GetBlobDataHandle() {

```

### match
```
...
 namespace blink { ...   >>> 
 base::span<const uint8_t> 
 WebSocketChannelImpl::Message::PendingPayload 
 ()  <<< ... } ...  
```
### patch
```
base::span<const uint8_t> WebSocketChannelImpl_ChromiumImpl::Message::PendingPayload()

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::Message::ConsumePendingPayload 
 (  <<< ... 
size_t bytes_consumed
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::Message::ConsumePendingPayload(

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::Message::DidCallSendMessage 
 WebSocketChannelImpl::Message::GetDidCallSendMessage() const 
 {  <<< ... 
return did_call_send_message_;
 ... } ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::Message::DidCallSendMessage
WebSocketChannelImpl_ChromiumImpl::Message::GetDidCallSendMessage() const {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::Message::SetDidCallSendMessage(
    WebSocketChannelImpl::Message::DidCallSendMessage did_call_send_message) 
 {  <<< ... 
did_call_send_message_ = did_call_send_message;
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::Message::SetDidCallSendMessage(
    WebSocketChannelImpl_ChromiumImpl::Message::DidCallSendMessage did_call_send_message) {

```

### match
```
...
 namespace blink { ...   >>> 
 uint16_t 
 WebSocketChannelImpl::Message::Code() const 
 {  <<< ... 
return code_;
 ... } ...  } ...  
```
### patch
```
uint16_t WebSocketChannelImpl_ChromiumImpl::Message::Code() const {

```

### match
```
...
 namespace blink { ...   >>> 
 String 
 WebSocketChannelImpl::Message::Reason() const 
 {  <<< ... 
return reason_;
 ... } ...  } ...  
```
### patch
```
String WebSocketChannelImpl_ChromiumImpl::Message::Reason() const {

```

### match
```
...
 namespace blink { ... 
std::unique_ptr<WebSocketChannel::SendCompletionWatcher>  >>> 
 WebSocketChannelImpl::Message::TakeSendCompletionWatcher() 
 {  <<< ... 
return std::move(watcher_);
 ... } ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::Message::TakeSendCompletionWatcher() {

```

### match
```
...
 namespace blink { ... 
std::unique_ptr<WebSocketChannel::SendCompletionWatcher>
WebSocketChannelImpl_ChromiumImpl::Message::TakeSendCompletionWatcher() {
	return std::move(watcher_);
}  >>> 
 // This could be done directly in WebSocketChannelImpl, but is a separate class  <<< ... 
// to make it easier to verify correctness.
 ... } ...  
```
### patch
```
// This could be done directly in WebSocketChannelImpl_ChromiumImpl, but is a separate class

```

### match
```
...
 namespace blink { ...   >>> 
 WebSocketChannelImpl::ConnectionCountTrackerHandle::CountStatus 
 WebSocketChannelImpl::ConnectionCountTrackerHandle::IncrementAndCheckStatus() 
 {  <<< ... 
DCHECK(!incremented_);
 ... } ...  } ...  
```
### patch
```
WebSocketChannelImpl_ChromiumImpl::ConnectionCountTrackerHandle::CountStatus
WebSocketChannelImpl_ChromiumImpl::ConnectionCountTrackerHandle::IncrementAndCheckStatus() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::ConnectionCountTrackerHandle::Decrement() 
 {  <<< ... 
if (incremented_) {
    incremented_ = false;
    const size_t old_count =
        g_connection_count.fetch_sub(1, std::memory_order_relaxed);
    DCHECK_NE(old_count, 0u);
  }
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::ConnectionCountTrackerHandle::Decrement() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::SendFromMemory 
 (  <<< ... 
MessageType type
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::SendFromMemory(

```

### match
```
...
 namespace blink { ...   >>> 
 bool 
 WebSocketChannelImpl::MaybeSendSynchronously 
 (  <<< ... 
MessageTypeForMojo frame_type
 ... ) ...  } ...  
```
### patch
```
bool WebSocketChannelImpl_ChromiumImpl::MaybeSendSynchronously(

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::ProcessSendQueue() 
 {  <<< ... 
// TODO(yhirano): This should be DCHECK_EQ(GetState(), State::kOpen).
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::ProcessSendQueue() {

```

### match
```
...
 namespace blink { ...   >>> 
 std::pair<bool, size_t> 
 WebSocketChannelImpl::SendMessageData 
 (  <<< ... 
base::span<const uint8_t> data
 ... ) ...  } ...  
```
### patch
```
std::pair<bool, size_t> WebSocketChannelImpl_ChromiumImpl::SendMessageData(

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::AbortAsyncOperations() 
 {  <<< ... 
if (blob_loader_) {
    blob_loader_->Cancel();
    blob_loader_.Clear();
  }
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::AbortAsyncOperations() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::HandleDidClose 
 ( 
 bool was_clean 
 ,  <<< ... 
uint16_t code
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::HandleDidClose(bool was_clean,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::OnCompletion 
 (  <<< ... 
const std::optional<WebString>& console_message
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::OnCompletion(

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::DidFinishLoadingBlob(MessageData data) 
 {  <<< ... 
DCHECK_EQ(GetState(), State::kOpen);
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::DidFinishLoadingBlob(MessageData data) {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::BlobTooLarge() 
 {  <<< ... 
DCHECK_EQ(GetState(), State::kOpen);
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::BlobTooLarge() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::DidFailLoadingBlob(FileErrorCode error_code) 
 {  <<< ... 
DCHECK_EQ(GetState(), State::kOpen);
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::DidFailLoadingBlob(FileErrorCode error_code) {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::TearDownFailedConnection() 
 {  <<< ... 
if (GetState() == State::kDisconnected) {
    return;
  }
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::TearDownFailedConnection() {

```

### match
```
...
 namespace blink { ...   >>> 
 bool 
 WebSocketChannelImpl::ShouldDisallowConnection(const KURL& url) 
 {  <<< ... 
SubresourceFilter* subresource_filter =
      GetBaseFetchContext()->GetSubresourceFilter();
 ... } ...  } ...  
```
### patch
```
bool WebSocketChannelImpl_ChromiumImpl::ShouldDisallowConnection(const KURL& url) {

```

### match
```
...
 namespace blink { ...   >>> 
 BaseFetchContext 
 * WebSocketChannelImpl::GetBaseFetchContext() const 
 {  <<< ... 
ResourceFetcher* resource_fetcher = execution_context_->Fetcher();
 ... } ...  } ...  
```
### patch
```
BaseFetchContext* WebSocketChannelImpl_ChromiumImpl::GetBaseFetchContext() const {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::OnReadable 
 ( 
 MojoResult result 
 ,  <<< ... 
const mojo::HandleSignalsState& state
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::OnReadable(MojoResult result,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::ConsumePendingDataFrames() 
 {  <<< ... 
DCHECK_EQ(GetState(), State::kOpen);
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::ConsumePendingDataFrames() {

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::ConsumeDataFrame 
 ( 
 bool fin 
 ,  <<< ... 
MessageTypeForMojo type
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::ConsumeDataFrame(bool fin,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::OnWritable 
 ( 
 MojoResult result 
 ,  <<< ... 
const mojo::HandleSignalsState& state
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::OnWritable(MojoResult result,

```

### match
```
...
 namespace blink { ...   >>> 
 base::span<const uint8_t> 
 WebSocketChannelImpl::ProduceData 
 (  <<< ... 
base::span<const uint8_t> data
 ... ) ...  } ...  
```
### patch
```
base::span<const uint8_t> WebSocketChannelImpl_ChromiumImpl::ProduceData(

```

### match
```
...
 namespace blink { ...   >>> 
 String 
 WebSocketChannelImpl::GetTextMessage 
 (  <<< ... 
const Vector<base::span<const uint8_t>>& chunks
 ... ) ...  } ...  
```
### patch
```
String WebSocketChannelImpl_ChromiumImpl::GetTextMessage(

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::OnConnectionError 
 ( 
 const base::Location& set_from 
 ,  <<< ... 
uint32_t custom_reason
 ... ) ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::OnConnectionError(const base::Location& set_from,

```

### match
```
...
 namespace blink { ...   >>> 
 void 
 WebSocketChannelImpl::Dispose() 
 {  <<< ... 
connection_count_tracker_handle_.Decrement();
 ... } ...  } ...  
```
### patch
```
void WebSocketChannelImpl_ChromiumImpl::Dispose() {

```

### match
```
...
 namespace blink { ... 
 std::ostream& operator<< ( ...   >>> 
 const WebSocketChannelImpl* channel 
 ) 
 { 
 return 
 ostream << "WebSocketChannelImpl "  <<< ... } ...  } ...  
```
### patch
```
                         const WebSocketChannelImpl_ChromiumImpl* channel) {
  return ostream << "WebSocketChannelImpl_ChromiumImpl "

```

### match
```
...
 namespace blink { ... 
 std::ostream& operator<<(std::ostream& ostream,
                                                  const WebSocketChannelImpl_ChromiumImpl* channel) { ... 
return ostream << "WebSocketChannelImpl_ChromiumImpl "
		<< static_cast<const void*>(channel);
 } 
 >>> 
 ... } ...  
```
### patch
```
// static
WebSocketChannelImpl* WebSocketChannelImpl::Create(
    ExecutionContext* execution_context,
    WebSocketChannelClient* client,
    SourceLocation* location) {
  auto* channel = MakeGarbageCollected<WebSocketChannelImpl>(execution_context,
                                                             client, location);
  channel->handshake_throttle_ =
      channel->GetBaseFetchContext()->CreateWebSocketHandshakeThrottle();
  return channel;
}

void WebSocketChannelImpl::TearDownFailedConnection() {
  if (base::FeatureList::IsEnabled(blink::features::kRestrictWebSocketsPool)) {
    websocket_in_use_tracker_.reset();
  }
  WebSocketChannelImpl_ChromiumImpl::TearDownFailedConnection();
}

bool WebSocketChannelImpl::ShouldDisallowConnection(const KURL& url) {
  if (base::FeatureList::IsEnabled(blink::features::kRestrictWebSocketsPool)) {
    const bool is_extension = CommonSchemeRegistry::IsExtensionScheme(
        execution_context_->GetSecurityOrigin()->Protocol().Ascii());
    if (!is_extension &&
        brave::GetBraveFarblingLevelFor(
            execution_context_,
            ContentSettingsType::BRAVE_WEBCOMPAT_WEB_SOCKETS_POOL,
            BraveFarblingLevel::OFF) != BraveFarblingLevel::OFF) {
      websocket_in_use_tracker_ =
          ResourcePoolLimiter::GetInstance().IssueResourceInUseTracker(
              execution_context_,
              ResourcePoolLimiter::ResourceType::kWebSocket);
      if (!websocket_in_use_tracker_) {
        return true;
      }
    }
  }
  return WebSocketChannelImpl_ChromiumImpl::ShouldDisallowConnection(url);
}

void WebSocketChannelImpl::Dispose() {
  if (base::FeatureList::IsEnabled(blink::features::kRestrictWebSocketsPool)) {
    websocket_in_use_tracker_.reset();
  }
  WebSocketChannelImpl_ChromiumImpl::Dispose();
}


```

