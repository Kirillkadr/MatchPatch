### match
```cpp
...
 
 namespace affiliations { ... 
 
 namespace { ... 
// none of the group's facets have change password URLs then those facets are
 // not inserted to the map. 
 >>> 
std::map<FacetURI, AffiliationServiceImpl::ChangePasswordUrlMatch>
CreateFacetUriToChangePasswordUrlMap(
    const std::vector<GroupedFacets>& groupings) {
  std::map<FacetURI, AffiliationServiceImpl::ChangePasswordUrlMatch> uri_to_url;
  for (const auto& grouped_facets : groupings) {
    for (const auto& facet : grouped_facets.facets) {
      // Affiliation server didn't generate it. Such facets can be skipped.
      if (facet.is_facet_synthesized) {
        continue;
      }
      uri_to_url[facet.uri] = AffiliationServiceImpl::ChangePasswordUrlMatch{
          .change_password_url = facet.change_password_url};
    }
  }
  return uri_to_url;
}
 ... } ...  } ...  
```
### patch
```cpp
#define AffiliationServiceImpl AffiliationServiceImpl_ChromiumImpl

```

### match
```cpp
...
 
 namespace affiliations { ... 
 
 base::WeakPtr<AffiliationService> AffiliationServiceImpl::AsWeakPtr() { ... 
return weak_ptr_factory_.GetWeakPtr();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
#undef AffiliationServiceImpl
void AffiliationServiceImpl::PrefetchChangePasswordURL(
    const GURL& urls,
    base::OnceClosure callback) {
  base::SequencedTaskRunner::GetCurrentDefault()->PostTask(FROM_HERE,
                                                           std::move(callback));
}
void AffiliationServiceImpl::Prefetch(const FacetURI& facet_uri,
                                      const base::Time& keep_fresh_until) {}

void AffiliationServiceImpl::RegisterSource(
    std::unique_ptr<AffiliationSource> source) {}

```

