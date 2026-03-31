### match
```cpp
...
 
 namespace content { ... 
 
 namespace { ... 
 
 void StartURLLoader(
    const network::ResourceRequest& request,
    FrameTreeNodeId frame_tree_node_id,
    mojo::PendingRemote<network::mojom::URLLoaderClient> client_remote,
    BrowserContext* browser_context) { ... 
// the value for |replacements| on the IO thread. Since |replacements| is
 // owned by |source| keep a reference to it in the callback. 
 >>> 
URLDataSource::GotDataCallback data_available_callback = base::BindOnce(
      DataAvailable, std::move(resource_response), replacements, replace_in_js,
      base::RetainedRef(source), std::move(client_remote),
      std::move(maybe_range), std::move(url_request_elapsed_timer));
 ... } ...  } ...  } ...  
```
### patch
```cpp
  URLDataSource::GotDataCallback unused_callback;
  if (range_or_error.has_value() &&
      source->source()->SupportsRangeRequests(request.url)) {
    URLDataSource::GotRangeDataCallback callback = base::BindOnce(
        RangeDataAvailable, request.url, std::move(resource_response),
        replacements, replace_in_js, base::RetainedRef(source),
        std::move(client_remote), base::OptionalFromExpected(range_or_error),
        std::move(url_request_elapsed_timer));
    source->source()->StartRangeDataRequest(
        request.url, wc_getter, range_or_error.value(), std::move(callback));
    return;
  }

```

### match
```cpp
...
 
 namespace content { ... 
 
 mojo::PendingRemote<network::mojom::URLLoaderFactory>
CreateWebUIURLLoaderFactory(RenderFrameHost* render_frame_host,
                            const std::string& scheme,
                            base::flat_set<std::string> allowed_hosts) { ... 
return WebUIURLLoaderFactory::CreateForFrame(
      FrameTreeNode::From(render_frame_host), scheme, std::move(allowed_hosts));
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
namespace {
void RangeDataAvailable(
    const GURL& url,
    network::mojom::URLResponseHeadPtr headers,
    const ui::TemplateReplacements* replacements,
    bool replace_in_js,
    scoped_refptr<URLDataSourceImpl> source,
    mojo::PendingRemote<network::mojom::URLLoaderClient> client_remote,
    std::optional<net::HttpByteRange> requested_range,
    base::ElapsedTimer url_request_elapsed_timer,
    URLDataSource::RangeDataResult result);

}  // namespace

namespace {

void RangeDataAvailable(
    const GURL& url,
    network::mojom::URLResponseHeadPtr headers,
    const ui::TemplateReplacements* replacements,
    bool replace_in_js,
    scoped_refptr<URLDataSourceImpl> source,
    mojo::PendingRemote<network::mojom::URLLoaderClient> client_remote,
    std::optional<net::HttpByteRange> requested_range,
    base::ElapsedTimer url_request_elapsed_timer,
    URLDataSource::RangeDataResult result) {
  TRACE_EVENT0("ui", "WebUIURLLoader::RangeDataAvailable");
  const auto& [bytes, range, total_size, mimetype] = result;

  // Fix up the response header in a HTTP Range spec
  // https://developer.mozilla.org/en-US/docs/Web/HTTP/Range_requests
  // The header should contain:
  // * "HTTP/1.1 206 Partial Content"
  // * "Accept-Ranges: bytes"
  // * "Content-Range: bytes 0-100/10000"  (0-100 is the range, 10000 is the
  //                                        total size. If total size is
  //                                        unknown, use "*")
  // * "Content-length: 10000" (the size of the whole file. Note that this is
  //                            different with what MDN says. But when
  //                            Content-length contains the range's size, then
  //                            the <video> won't be played). See also,
  //    https://source.chromium.org/chromium/chromium/src/+/main:content/browser/webui/web_ui_url_loader_factory.cc;l=143-147;drc=2af756c3ed38c6fb6472c821fc71d79b07984cac
  //
  // * "Content-type": "video/mp4" (or the correct mime type)
  if (bytes && range.IsValid()) {
    headers->headers->UpdateWithNewRange(range, total_size,
                                         /*replace_status_line*/ true);
    headers->headers->SetHeader("Accept-Ranges", "bytes");
    headers->headers->SetHeader("Content-Type", mimetype);
    headers->headers->SetHeader("Content-Length",
                                base::NumberToString(bytes->size()));
    headers->content_length = bytes->size();
    if (total_size > 0) {
      headers->headers->SetHeader("Content-Length",
                                  base::NumberToString(total_size));
      headers->content_length = total_size;
    }

    headers->parsed_headers =
        network::PopulateParsedHeaders(headers->headers.get(), url);
    requested_range.reset();
  }

  DataAvailable(std::move(headers), replacements, replace_in_js, source,
                std::move(client_remote), requested_range,
                std::move(url_request_elapsed_timer), bytes);
}

}  // namespace

```

