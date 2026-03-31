### match
```cpp
...
 
 # ifndef ... 
#include <string_view>

 #include <vector>
 
 >>> 
#include "base/memory/raw_ptr.h"

 ... 
```
### patch
```cpp
#include <optional>
#include <string>
#include "content/browser/speech/speech_recognition_engine.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
// after closing the upstream). Both streams are guaranteed to be closed when
 // |EndRecognition| call is issued. 
 >>> 
class CONTENT_EXPORT NetworkSpeechRecognitionEngineImpl
    : public SpeechRecognitionEngine,
      public speech::UpstreamLoaderClient,
      public speech::DownstreamLoaderClient {
 public:
  // Network engine configuration.
  struct CONTENT_EXPORT Config {
    Config();
    ~Config();

    std::string language;
    std::vector<media::mojom::SpeechRecognitionGrammar> grammars;
    bool filter_profanities = false;
    bool continuous = true;
    bool interim_results = true;
    uint32_t max_hypotheses;
    std::string origin_url;
    int audio_sample_rate;
    int audio_num_bits_per_sample;
    std::string auth_token;
    std::string auth_scope;
    scoped_refptr<SpeechRecognitionSessionPreamble> preamble;
  };
 ... } ...  } ...  
```
### patch
```cpp
#define NetworkSpeechRecognitionEngineImpl \
  NetworkSpeechRecognitionEngineImpl_ChromiumImpl

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
NetworkSpeechRecognitionEngineImpl& operator=(
      const NetworkSpeechRecognitionEngineImpl&) = delete;
 ~NetworkSpeechRecognitionEngineImpl() override 
 ; 
 >>> 
// Sets the URL requests are sent to for tests.
 ... } ...  
```
### patch
```cpp
#undef NetworkSpeechRecognitionEngineImpl

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
SEQUENCE_CHECKER(sequence_checker_);
 } 
 ; 
 >>> 
}
 ... 
```
### patch
```cpp
class CONTENT_EXPORT NetworkSpeechRecognitionEngineImpl
    : public NetworkSpeechRecognitionEngineImpl_ChromiumImpl {
 public:
  NetworkSpeechRecognitionEngineImpl(
      scoped_refptr<network::SharedURLLoaderFactory> shared_url_loader_factory);
  ~NetworkSpeechRecognitionEngineImpl() override;
  void StartRecognition() override;

 private:
  void OnStickySessionReady(std::unique_ptr<network::SimpleURLLoader> loader,
                            std::optional<std::string> response_body);

  scoped_refptr<network::SharedURLLoaderFactory> shared_url_loader_factory_;
  base::WeakPtrFactory<NetworkSpeechRecognitionEngineImpl> weak_ptr_factory_{
      this};
};

```

