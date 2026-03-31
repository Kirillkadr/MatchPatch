### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 class CONTENT_EXPORT URLDataSource { ... 
// originated from a worker or if the frame has destructed it will return
 // null. 
 >>> 
virtual void StartDataRequest(const GURL& url,
                                const WebContents::Getter& wc_getter,
                                GotDataCallback callback) = 0;
 ... } ...  } ...  
```
### patch
```cpp
  virtual void StartDataRequest_Unused() {}

  struct CONTENT_EXPORT RangeDataResult {
    RangeDataResult();
    RangeDataResult(RangeDataResult&&) noexcept;
    RangeDataResult& operator=(RangeDataResult&&) noexcept;
    ~RangeDataResult();

    scoped_refptr<base::RefCountedMemory> buffer;
    net::HttpByteRange range;
    int64_t file_size = 0;
    std::string mime_type;
  };
  using GotRangeDataCallback = base::OnceCallback<void(RangeDataResult)>;

  virtual void StartRangeDataRequest(
      const GURL& url, const WebContents::Getter& wc_getter,
      const net::HttpByteRange& range, GotRangeDataCallback callback) {}

  virtual bool SupportsRangeRequests(const GURL& url) const;


```

