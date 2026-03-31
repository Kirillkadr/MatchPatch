### match
```cpp
...
 
 # ifndef ... 
 
 namespace autofill { ... 
VotesUploader& GetVotesUploader() final;  >>> 
 AutofillOptimizationGuideDecider* GetAutofillOptimizationGuideDecider()
      const final;  <<< 
FieldClassificationModelHandler* GetAutofillFieldClassificationModelHandler()
      final;
 ... } ...  
```
### patch
```cpp
  AutofillOptimizationGuideDecider* GetAutofillOptimizationGuideDecider() const override;


```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace autofill { ... 
ActorKeyMetricsRecorder* GetActorKeyMetricsRecorder() final;  >>> 
 bool IsAutofillEnabled() const final;  <<< 
bool IsAutofillProfileEnabled() const final;
 ... } ...  
```
### patch
```cpp
  bool  IsAutofillEnabled() const override;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace autofill { ... 
bool IsAutofillProfileEnabled() const final;  >>> 
 bool IsAutocompleteEnabled() const final;  <<< 
bool IsWalletPublicPassStorageEnabled() const final;
 ... } ...  
```
### patch
```cpp
  bool IsAutocompleteEnabled() const override; 

```

