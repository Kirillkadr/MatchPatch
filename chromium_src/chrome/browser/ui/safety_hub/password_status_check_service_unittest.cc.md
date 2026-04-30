### match
```cpp
...
 
 INSTANTIATE_TEST_SUITE_P ( ... 
 testing::Range(0, 7) 
 ) 
 ; 
 >>> 
 ... 
```
### patch
```cpp

TEST_P(PasswordStatusCheckServiceParameterizedCardTest,
       PasswordCardDataIsMarkedSafe) {
  // Based on test parameters, add different credential issues to the store.
  if (include_weak()) {
    profile_store().AddLogin(WeakForm());
  }
  if (include_compromised()) {
    profile_store().AddLogin(LeakedForm());
  }
  if (include_reused()) {
    profile_store().AddLogin(ReusedForm1());
    profile_store().AddLogin(ReusedForm2());
  }

  // The password card data should always be marked safe
  base::DictValue dict;
  dict.Set(safety_hub::kCardStateKey,
           static_cast<int>(safety_hub::SafetyHubCardState::kSafe));
  EXPECT_EQ(dict, service()->GetPasswordCardData(signed_in()));
}

```

