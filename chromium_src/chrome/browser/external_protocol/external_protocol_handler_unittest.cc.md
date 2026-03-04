### match
```
...
#else
#include "components/web_modal/web_contents_modal_dialog_manager.h"

 #endif 
 // BUILDFLAG(IS_ANDROID) 
 >>> 
class FakeExternalProtocolHandlerWorker
    : public shell_integration::DefaultSchemeClientWorker {
 public:
  FakeExternalProtocolHandlerWorker(
      const GURL& url,
      shell_integration::DefaultWebClientState os_state,
      const std::u16string& program_name)
      : shell_integration::DefaultSchemeClientWorker(url),
        os_state_(os_state),
        program_name_(program_name) {}

 private:
  ~FakeExternalProtocolHandlerWorker() override = default;

  shell_integration::DefaultWebClientState CheckIsDefaultImpl() override {
    return os_state_;
  }

  std::u16string GetDefaultClientNameImpl() override { return program_name_; }

  void SetAsDefaultImpl(base::OnceClosure on_finished_callback) override {
    std::move(on_finished_callback).Run();
  }

  shell_integration::DefaultWebClientState os_state_;
  std::u16string program_name_;
}
 ... 
```
### patch
```
class ExternalProtocolHandlerTest : public testing::Test {
 protected:
  void SetUp() override { profile_ = std::make_unique<TestingProfile>(); }

  content::BrowserTaskEnvironment task_environment_;
  std::unique_ptr<TestingProfile> profile_;
};

TEST_F(ExternalProtocolHandlerTest, TestGetBlockStateMailto) {
  ExternalProtocolHandler::BlockState block_state =
      ExternalProtocolHandler::GetBlockState("mailto", nullptr, profile_.get());
  EXPECT_EQ(ExternalProtocolHandler::UNKNOWN, block_state);
}


```

