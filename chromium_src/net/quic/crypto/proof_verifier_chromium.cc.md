### match
```
...
 namespace net { ... 
 int ProofVerifierChromium::Job::DoVerifyCertComplete(int result) { ...   >>> 
 transport_security_state_->ShouldSSLErrorsBeFatal(hostname_) 
 ;  <<< ... } ...  } ...  
```
### patch
```
      transport_security_state_->ShouldSSLErrorsBeFatal(proof_verifier_->network_anonymization_key_, hostname_);

```

