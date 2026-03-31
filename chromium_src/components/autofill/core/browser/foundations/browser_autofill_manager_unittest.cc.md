### match
```cpp
...
 
 namespace autofill { ...
 
 >>> 
 } ...  ```
### patch
```cpp
}  // namespace

namespace {

// Test that if a form is mixed content we show a warning instead of any
// suggestions.
TEST_F(BrowserAutofillManagerTest, Onion_MixedFormHttps) {
  // Set up our form data.
  FormData form;
  form.set_name(u"MyForm");
  form.set_url(GURL("https://myform.onion/form.html"));
  form.set_action(GURL("http://myform.com/submit.html"));
  form.set_fields({CreateTestFormField("Name on Card", "nameoncard", "",
                                       FormControlType::kInputText)});

  OnAskForValuesToFill(form, form.fields()[0]);

  // Test that we sent the right values to the external delegate.
  external_delegate()->CheckSuggestions(
      form.fields().back().global_id(),
      {Suggestion(l10n_util::GetStringUTF8(IDS_AUTOFILL_WARNING_MIXED_FORM), "",
                  Suggestion::Icon::kNoIcon,
                  SuggestionType::kMixedFormMessage)});
}

TEST_F(BrowserAutofillManagerTest, Onion_MixedFormHttp) {
  // Set up our form data.
  FormData form;
  form.set_name(u"MyForm");
  form.set_url(GURL("http://myform.onion/form.html"));
  form.set_action(GURL("http://myform.com/submit.html"));
  form.set_fields({CreateTestFormField("Name on Card", "nameoncard", "",
                                       FormControlType::kInputText)});

  OnAskForValuesToFill(form, form.fields()[0]);

  // Test that we sent the right values to the external delegate.
  external_delegate()->CheckSuggestions(
      form.fields().back().global_id(),
      {Suggestion(l10n_util::GetStringUTF8(IDS_AUTOFILL_WARNING_MIXED_FORM), "",
                  Suggestion::Icon::kNoIcon,
                  SuggestionType::kMixedFormMessage)});
}

TEST_F(BrowserAutofillManagerTest, Onion_MixedFormHttpSubdomain) {
  // Set up our form data.
  FormData form;
  form.set_name(u"MyForm");
  form.set_url(GURL("http://a.myform.onion/form.html"));
  form.set_action(GURL("http://myform.com/submit.html"));
  form.set_fields({CreateTestFormField("Name on Card", "nameoncard", "",
                                       FormControlType::kInputText)});

  OnAskForValuesToFill(form, form.fields()[0]);

  // Test that we sent the right values to the external delegate.
  external_delegate()->CheckSuggestions(
      form.fields().back().global_id(),
      {Suggestion(l10n_util::GetStringUTF8(IDS_AUTOFILL_WARNING_MIXED_FORM), "",
                  Suggestion::Icon::kNoIcon,
                  SuggestionType::kMixedFormMessage)});
}

// Test that if a form is not mixed content we show suggestions.
TEST_F(BrowserAutofillManagerTest, Onion_NonMixedForm) {
  // Set up our form data.
  FormData form;
  form.set_name(u"MyForm");
  form.set_url(GURL("http://myform.onion/form.html"));
  form.set_action(GURL("https://myform.com/submit.html"));
  form.set_fields({CreateTestFormField("Name on Card", "nameoncard", "",
                                       FormControlType::kInputText)});

  OnAskForValuesToFill(form, form.fields()[0]);

  // Check there is no warning.
  EXPECT_FALSE(external_delegate()->on_suggestions_returned_seen());
}


```

