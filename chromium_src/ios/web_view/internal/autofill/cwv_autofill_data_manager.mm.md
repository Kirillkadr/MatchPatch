### match
```cpp
...
// found in the LICENSE file.
 #import <memory>
 
 >>> 
#import "base/functional/bind.h"

 ... 
```
### patch
```cpp
#pragma clang diagnostic push
#pragma clang diagnostic ignored "-Wnullability-completeness"

```

### match
```cpp
...
:(nullable NSString*)newPassword
             timestamp:(NSDate*)timestamp {
  password_manager::PasswordForm* passwordForm =
      [password internalPasswordForm];
  passwordForm->date_password_modified = base::Time::FromNSDate(timestamp);

  // Only change the password if it actually changed and not empty.
  if (newPassword && newPassword.length > 0 &&
      ![newPassword isEqualToString:password.password]) {
    passwordForm->password_value = base::SysNSStringToUTF16(newPassword);
  }

  // Because a password's primary key depends on its username, changing the
  // username requires that |UpdateLoginWithPrimaryKey| is called instead.
  if (newUsername && newUsername.length > 0 &&
      ![newUsername isEqualToString:password.username]) {
    // Make a local copy of the old password before updating it.
    auto oldPasswordForm = *passwordForm;
    passwordForm->username_value = base::SysNSStringToUTF16(newUsername);
    auto newPasswordForm = *passwordForm;
    _passwordStore->UpdateLoginWithPrimaryKey(newPasswordForm, oldPasswordForm);
  } else {
    _passwordStore->UpdateLogin(*passwordForm);
  }
}

- (void)deletePassword:(CWVPassword*)password {
  _passwordStore->RemoveLogin(FROM_HERE, *[password internalPasswordForm]);
}

- (void)addNewPasswordForUsername:(NSString*)username
                         password:(NSString*)password
                             site:(NSString*)site
                        timestamp:(NSDate*)timestamp {
  password_manager::PasswordForm form;

  DCHECK_GT(username.length, 0ul);
  DCHECK_GT(password.length, 0ul);
  GURL url(base::SysNSStringToUTF8(site));
  DCHECK(url.is_valid());

  form.url = password_manager_util::StripAuthAndParams(url);
  form.signon_realm = form.url.DeprecatedGetOriginAsURL().spec();
  form.username_value = base::SysNSStringToUTF16(username);
  form.password_value = base::SysNSStringToUTF16(password);
  form.date_created = base::Time::FromNSDate(timestamp);

  _passwordStore->AddLogin(form);
}

- (void)addNewPasswordForUsername:(NSString*)username
                serviceIdentifier:(NSString*)serviceIdentifier
               keychainIdentifier:(NSString*)keychainIdentifier
                        timestamp:(NSDate*)timestamp {
  password_manager::PasswordForm form;

  GURL url(base::SysNSStringToUTF8(serviceIdentifier));
  DCHECK(url.is_valid());

  form.url = password_manager_util::StripAuthAndParams(url);
  form.signon_realm = form.url.DeprecatedGetOriginAsURL().spec();
  form.username_value = base::SysNSStringToUTF16(username);
  form.keychain_identifier = base::SysNSStringToUTF8(keychainIdentifier);
  form.date_created = base::Time::FromNSDate(timestamp);

  _passwordStore->AddLogin(form);
}

#pragma mark - Private Methods

- (BOOL)isPasswordAffiliationEnabled {
  return _isPasswordAffiliationEnabled;
}

- (void)handlePasswordStoreLoginsAdded:(NSArray<CWVPassword*>*)added
                               updated:(NSArray<CWVPassword*>*)updated
                               removed:(NSArray<CWVPassword*>*)removed {
  for (id<CWVAutofillDataManagerObserver> observer in _observers) {
    [observer autofillDataManager:self
        didChangePasswordsByAdding:added
                          updating:updated
                          removing:removed];
  }
}

- (void)handlePasswordStoreResults:(NSArray<CWVPassword*>*)passwords {
  for (CWVFetchPasswordsCompletionHandler completionHandler in
           _fetchPasswordsCompletionHandlers) {
    completionHandler(passwords);
  }
  [_fetchPasswordsCompletionHandlers removeAllObjects];
  _passwordStoreConsumer.reset();
}

- (void)personalDataDidChange {
  // Invoke completionHandlers if they are still outstanding.
  if (_personalDataManager->IsDataLoaded()) {
    if (_fetchProfilesCompletionHandlers.count > 0) {
      NSArray<CWVAutofillProfile*>* profiles = [self profiles];
      for (CWVFetchProfilesCompletionHandler completionHandler in
               _fetchProfilesCompletionHandlers) {
        completionHandler(profiles);
      }
      [_fetchProfilesCompletionHandlers removeAllObjects];
    }
    if (_fetchCreditCardsCompletionHandlers.count > 0) {
      NSArray<CWVCreditCard*>* creditCards = [self creditCards];
      for (CWVFetchCreditCardsCompletionHandler completionHandler in
               _fetchCreditCardsCompletionHandlers) {
        completionHandler(creditCards);
      }
      [_fetchCreditCardsCompletionHandlers removeAllObjects];
    }
  }
  for (id<CWVAutofillDataManagerObserver> observer in _observers) {
    [observer autofillDataManagerDataDidChange:self];
  }
}

- (NSArray<CWVAutofillProfile*>*)profiles {
  NSMutableArray* profiles = [NSMutableArray array];
  for (const autofill::AutofillProfile* internalProfile :
       _personalDataManager->address_data_manager().GetProfiles()) {
    CWVAutofillProfile* profile =
        [[CWVAutofillProfile alloc] initWithProfile:*internalProfile];
    [profiles addObject:profile];
  }
  return [profiles copy];
}

- (NSArray<CWVCreditCard*>*)creditCards {
  std::vector<const autofill::CreditCard*> fetchedCards =
      _personalDataManager->payments_data_manager().GetCreditCards();

  NSMutableArray* creditCards = [NSMutableArray array];
  for (const autofill::CreditCard* card : fetchedCards) {
    if (card->virtual_card_enrollment_state() ==
        autofill::CreditCard::VirtualCardEnrollmentState::kEnrolled) {
      autofill::CreditCard virtualCard =
          autofill::CreditCard::CreateVirtualCard(*card);
      CWVCreditCard* cwvVirtualCard =
          [[CWVCreditCard alloc] initWithCreditCard:virtualCard];
      [creditCards addObject:cwvVirtualCard];
      // Do not `continue` here. Enrolled cards should be added twice, once as
      // a virtual card and once as a regular card, to allow the user to choose.
    }
    CWVCreditCard* cwvCard = [[CWVCreditCard alloc] initWithCreditCard:*card];
    [creditCards addObject:cwvCard];
  }
  return [creditCards copy];
}

- (void)shutDown {
  _personalDataManager->RemoveObserver(
      _personalDataManagerObserverBridge.get());
  _passwordStore->RemoveObserver(_passwordStoreObserver.get());
}


 @ 
 end 
 >>> 
 ... 
```
### patch
```cpp
// Helper category to expose the underlying `PersonalDataManager` so it may be
// used in //brave/ios/web_view targets to expose functionality missing from
// CWVAutofillDataManager
@implementation CWVAutofillDataManager (Internal)

- (autofill::PersonalDataManager*)personalDataManager {
  return _personalDataManager;
}

@end
```

