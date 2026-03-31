### match
```cpp
...
 
 namespace signin { ... 
INSTANTIATE_TEST_SUITE_P(
    ,
    ComputeProfileMenuAvatarButtonPromoInfoParamTest,
    testing::ValuesIn(
        {ProfileMenuAvatarButtonPromoInfo::Type::kHistorySyncPromo,
         ProfileMenuAvatarButtonPromoInfo::Type::kBatchUploadPromo,
         ProfileMenuAvatarButtonPromoInfo::Type::kBatchUploadBookmarksPromo,
         ProfileMenuAvatarButtonPromoInfo::Type::
             kBatchUploadWindows10DepreciationPromo,
         ProfileMenuAvatarButtonPromoInfo::Type::kSyncPromo,
         ProfileMenuAvatarButtonPromoInfo::Type::kSigninPromo}));
 #endif 
 // BUILDFLAG(ENABLE_DICE_SUPPORT) 
 >>> 
 ... } ...  
```
### patch
```cpp
#if BUILDFLAG(ENABLE_DICE_SUPPORT)

// Creating a derived class, so disabling
// `ShowSigninPromoTestExplicitBrowserSignin` in filter files won't affect these
// disable tests.
class ShowSigninPromoTestExplicitBrowserSigninIsDisabled
    : public ShowSigninPromoTestWithFeatureFlags {};

TEST_F(ShowSigninPromoTestExplicitBrowserSigninIsDisabled,
       ShowPromoWithNoAccount) {
  EXPECT_FALSE(ShouldShowPasswordSignInPromo(*profile()));
}

TEST_F(ShowSigninPromoTestExplicitBrowserSigninIsDisabled,
       ShowPromoWithWebSignedInAccount) {
  MakeAccountAvailable(identity_manager(), "test@email.com");
  EXPECT_FALSE(ShouldShowPasswordSignInPromo(*profile()));
}

TEST_F(ShowSigninPromoTestExplicitBrowserSigninIsDisabled,
       ShowPromoWithSignInPendingAccount) {
  AccountInfo info = MakePrimaryAccountAvailable(
      identity_manager(), "test@email.com", ConsentLevel::kSignin);
  signin::SetInvalidRefreshTokenForPrimaryAccount(identity_manager());
  EXPECT_FALSE(ShouldShowPasswordSignInPromo(*profile()));
}

TEST_F(ShowSigninPromoTestExplicitBrowserSigninIsDisabled,
       DoNotShowAddressPromo) {
  ASSERT_FALSE(ShouldShowAddressSignInPromo(*profile(), CreateAddress()));
}

TEST_F(ShowSigninPromoTestExplicitBrowserSigninIsDisabled,
       DoNotShowBookmarkPromo) {
  ASSERT_FALSE(ShouldShowBookmarkSignInPromo(*profile()));
}

TEST_F(ShowSigninPromoTestExplicitBrowserSigninIsDisabled,
       ShowExtensionsPromoWithNoAccount) {
  EXPECT_FALSE(ShouldShowExtensionSignInPromo(*profile(), *CreateExtension()));
}

#endif  // BUILDFLAG(ENABLE_DICE_SUPPORT)

```

