### match
```cpp

...
 namespace net { ... 
 int ProofVerifierChromium::Job::DoVerifyCertComplete(int result) { ...   >>> 
 transport_security_state_->ShouldSSLErrorsBeFatal(hostname_) 
 ;  <<< ... } ...  } ...  
```
### patch
```cpp

      transport_security_state_->ShouldSSLErrorsBeFatal(proof_verifier_->network_anonymization_key_, hostname_);

```

