### match
```cpp
...
 
 namespace content { ... 
bool URLDataSource::ShouldReplaceI18nInJS() {
  return false;
}
 } 
 // namespace content 
 >>> 
 ... 
```
### patch
```cpp

namespace content {

URLDataSource::RangeDataResult::RangeDataResult() = default;
URLDataSource::RangeDataResult::RangeDataResult(RangeDataResult&&) noexcept =
    default;
URLDataSource::RangeDataResult& URLDataSource::RangeDataResult::operator=(
    URLDataSource::RangeDataResult&&) noexcept = default;
URLDataSource::RangeDataResult::~RangeDataResult() = default;

bool URLDataSource::SupportsRangeRequests(const GURL& url) const {
  return false;
}

}  // namespace content

```

