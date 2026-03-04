### match
```
...
 
 # ifndef ... 
 
 class ProfileWriter : public base::RefCountedThreadSafe<ProfileWriter> { ... 
virtual void AddKeywords(
      TemplateURLService::OwnedTemplateURLVector template_urls,
      bool unique_on_host_and_path);
 // Adds the imported autocomplete entries to the autofill database. 
 >>> 
virtual void AddAutocompleteFormDataEntries(
      const std::vector<autofill::AutocompleteEntry>& autocomplete_entries);
 ... } ...  
```
### patch
```
  virtual void AddCreditCard(const std::u16string& name_on_card,
                const std::u16string& expiration_month,
                const std::u16string& expiration_year,
                const std::u16string& decrypted_card_number,
                const std::string& origin);                  

```

