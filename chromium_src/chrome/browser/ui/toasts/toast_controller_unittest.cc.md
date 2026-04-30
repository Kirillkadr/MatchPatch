### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToast) { ... 
 
 registry->RegisterToast ( ...   >>> 
 ToastId::kLinkCopied 
 ,  <<< 
ToastSpecification::Builder(vector_icons::kEmailIcon, kTestStringResId)
          .Build()
 ... ) ...  } ...  
```
### patch
```cpp
      ToastId::kLinkToHighlightCopied,

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToast) { ... 
EXPECT_FALSE(controller->IsShowingToast());  >>> 
 EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkCopied));  <<< 
EXPECT_CALL(*controller, CreateToast);
 ... } ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkToHighlightCopied));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToast) { ... 
EXPECT_CALL(*controller, CreateToast);  >>> 
 EXPECT_TRUE(controller->MaybeShowToast(ToastParams(ToastId::kLinkCopied)));  <<< 
::testing::Mock::VerifyAndClear(controller.get());
 ... } ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->MaybeShowToast(ToastParams(ToastId::kLinkToHighlightCopied)));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToast) { ... 
EXPECT_TRUE(controller->IsShowingToast());  >>> 
 EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkCopied));  <<<  ...} ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkToHighlightCopied));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToastWithBodyStringOverride) { ... 
 
 registry->RegisterToast ( ...   >>> 
 ToastId::kLinkCopied 
 ,  <<< 
ToastSpecification::Builder(vector_icons::kEmailIcon).Build()
 ... ) ...  } ...  
```
### patch
```cpp
      ToastId::kLinkToHighlightCopied,

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToastWithBodyStringOverride) { ... 
EXPECT_FALSE(controller->IsShowingToast());  >>> 
 EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkCopied));  <<< 
EXPECT_CALL(*controller, CreateToast);
 ... } ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkToHighlightCopied));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToastWithBodyStringOverride) { ... 
EXPECT_CALL(*controller, CreateToast);  >>> 
 ToastParams params = ToastParams(ToastId::kLinkCopied);  <<< 
params.body_string_override = u"Some toast body";
 ... } ...  
```
### patch
```cpp
  ToastParams params = ToastParams(ToastId::kLinkToHighlightCopied);

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToastWithBodyStringOverride) { ... 
EXPECT_TRUE(controller->IsShowingToast());  >>> 
 EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkCopied));  <<<  ...} ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkToHighlightCopied));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToastWithImage) { ... 
 
 registry->RegisterToast ( ...   >>> 
 ToastId::kLinkCopied 
 ,  <<< 
ToastSpecification::Builder(vector_icons::kEmailIcon, kTestStringResId)
          .Build()
 ... ) ...  } ...  
```
### patch
```cpp
      ToastId::kLinkToHighlightCopied,

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToastWithImage) { ... 
EXPECT_FALSE(controller->IsShowingToast());  >>> 
 EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkCopied));  <<< 
EXPECT_CALL(*controller, CreateToast);
 ... } ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkToHighlightCopied));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToastWithImage) { ... 
EXPECT_CALL(*controller, CreateToast);  >>> 
 ToastParams params = ToastParams(ToastId::kLinkCopied);  <<< 
params.image_override =
      ui::ImageModel::FromImage(gfx::test::CreateImage(16, 16, 0xff0000));
 ... } ...  
```
### patch
```cpp
  ToastParams params = ToastParams(ToastId::kLinkToHighlightCopied);

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ShowToastWithImage) { ... 
EXPECT_TRUE(controller->IsShowingToast());  >>> 
 EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkCopied));  <<<  ...} ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkToHighlightCopied));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ToastAutomaticallyCloses) { ... 
 
 registry->RegisterToast ( ...   >>> 
 ToastId::kLinkCopied 
 ,  <<< 
ToastSpecification::Builder(vector_icons::kEmailIcon, kTestStringResId)
          .Build()
 ... ) ...  } ...  
```
### patch
```cpp
      ToastId::kLinkToHighlightCopied,

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ToastAutomaticallyCloses) { ... 
EXPECT_CALL(*controller, CreateToast);  >>> 
 EXPECT_TRUE(controller->MaybeShowToast(ToastParams(ToastId::kLinkCopied)));  <<< 
::testing::Mock::VerifyAndClear(controller.get());
 ... } ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->MaybeShowToast(ToastParams(ToastId::kLinkToHighlightCopied)));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ToastCloseCallbackTriggered) { ... 
 
 registry->RegisterToast ( ...   >>> 
 ToastId::kLinkCopied 
 ,  <<< 
ToastSpecification::Builder(vector_icons::kEmailIcon, kTestStringResId)
          .Build()
 ... ) ...  } ...  
```
### patch
```cpp
      ToastId::kLinkToHighlightCopied,

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ToastCloseCallbackTriggered) { ... 
EXPECT_CALL(*controller, CreateToast);  >>> 
 ToastParams params = ToastParams(ToastId::kLinkCopied);  <<< 
bool callback_called = false;
 ... } ...  
```
### patch
```cpp
  ToastParams params = ToastParams(ToastId::kLinkToHighlightCopied);

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ToastWithActionButtonAutomaticallyCloses) { ... 
 
 registry->RegisterToast ( ...   >>> 
 ToastId::kLinkCopied 
 ,  <<< 
ToastSpecification::Builder(vector_icons::kEmailIcon, kTestStringResId)
          .Build()
 ... ) ...  } ...  
```
### patch
```cpp
      ToastId::kLinkToHighlightCopied,

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, ToastWithActionButtonAutomaticallyCloses) { ... 
EXPECT_CALL(*controller, CreateToast);  >>> 
 EXPECT_TRUE(controller->MaybeShowToast(ToastParams(ToastId::kLinkCopied)));  <<< 
::testing::Mock::VerifyAndClear(controller.get());
 ... } ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->MaybeShowToast(ToastParams(ToastId::kLinkToHighlightCopied)));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, CloseTimerResetsWhenToastShown) { ... 
 
 registry->RegisterToast ( ...   >>> 
 ToastId::kLinkCopied 
 ,  <<< 
ToastSpecification::Builder(vector_icons::kEmailIcon, kTestStringResId)
          .Build()
 ... ) ...  } ...  
```
### patch
```cpp
      ToastId::kLinkToHighlightCopied,

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, CloseTimerResetsWhenToastShown) { ... 
 
 registry->RegisterToast ( ...   >>> 
 ToastId::kImageCopied 
 ,  <<< 
ToastSpecification::Builder(vector_icons::kEmailIcon, kTestStringResId)
          .Build()
 ... ) ...  } ...  
```
### patch
```cpp
      ToastId::kClearBrowsingData,

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, CloseTimerResetsWhenToastShown) { ... 
EXPECT_CALL(*controller, CreateToast);  >>> 
 EXPECT_TRUE(controller->MaybeShowToast(ToastParams(ToastId::kLinkCopied)));  <<< 
::testing::Mock::VerifyAndClear(controller.get());
 ... } ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->MaybeShowToast(ToastParams(ToastId::kLinkToHighlightCopied)));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, CloseTimerResetsWhenToastShown) { ... 
EXPECT_CALL(*controller, CreateToast);  >>> 
 EXPECT_TRUE(controller->MaybeShowToast(ToastParams(ToastId::kImageCopied)));  <<< 
::testing::Mock::VerifyAndClear(controller.get());
 ... } ...  
```
### patch
```cpp
  EXPECT_TRUE(controller->MaybeShowToast(ToastParams(ToastId::kClearBrowsingData)));

```

### match
```cpp
...
 
 TEST_F(ToastControllerUnitTest, CloseTimerResetsWhenToastShown) { ... 
EXPECT_TRUE(controller->IsShowingToast());
 } 
 >>> 
 ... 
```
### patch
```cpp
TEST_F(ToastControllerUnitTest, NeverShowToastForLinkCopied) {
  ToastRegistry* const registry = toast_registry();
  registry->RegisterToast(
      ToastId::kLinkCopied,
      ToastSpecification::Builder(vector_icons::kEmailIcon, 0).Build());

  auto controller = std::make_unique<TestToastController>(registry);

  EXPECT_FALSE(controller->IsShowingToast());
  EXPECT_TRUE(controller->CanShowToast(ToastId::kLinkCopied));
  EXPECT_FALSE(controller->MaybeShowToast(ToastParams(ToastId::kLinkCopied)));
  EXPECT_FALSE(controller->IsShowingToast());
}

TEST_F(ToastControllerUnitTest, NeverShowToastForImageCopied) {
  ToastRegistry* const registry = toast_registry();
  registry->RegisterToast(
      ToastId::kImageCopied,
      ToastSpecification::Builder(vector_icons::kEmailIcon, 0).Build());

  auto controller = std::make_unique<TestToastController>(registry);

  EXPECT_FALSE(controller->IsShowingToast());
  EXPECT_TRUE(controller->CanShowToast(ToastId::kImageCopied));
  EXPECT_FALSE(controller->MaybeShowToast(ToastParams(ToastId::kImageCopied)));
  EXPECT_FALSE(controller->IsShowingToast());
}

TEST_F(ToastControllerUnitTest, NeverShowToastForAddedToReadingList) {
  ToastRegistry* const registry = toast_registry();
  registry->RegisterToast(
      ToastId::kAddedToReadingList,
      ToastSpecification::Builder(vector_icons::kEmailIcon, 0).Build());

  auto controller = std::make_unique<TestToastController>(registry);

  EXPECT_FALSE(controller->IsShowingToast());
  EXPECT_TRUE(controller->CanShowToast(ToastId::kAddedToReadingList));
  EXPECT_FALSE(
      controller->MaybeShowToast(ToastParams(ToastId::kAddedToReadingList)));
  EXPECT_FALSE(controller->IsShowingToast());
}

```

