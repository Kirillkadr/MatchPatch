### match
```
...
>>>
 void 
 RegisterTrustTokenKeyCommitmentsComponentIfTrustTokensEnabled 
 (  <<< ... 
ComponentUpdateService* cus
 ... ) ...  
```
### patch
```
void RegisterTrustTokenKeyCommitmentsComponentIfTrustTokensEnabled_ChromiumImpl(

```

### match
```
...
 namespace component_updater { ... 
 void RegisterTrustTokenKeyCommitmentsComponentIfTrustTokensEnabled_ChromiumImpl(
ComponentUpdateService* cus) { ... 
installer->Register(cus, base::OnceClosure());
 } 
 >>> 
 ... } ...  
```
### patch
```
/ We do not support TrustTokens aka PrivateStateTokens aka FeldgePst
void RegisterTrustTokenKeyCommitmentsComponentIfTrustTokensEnabled(
    ComponentUpdateService* cus) {}


```

