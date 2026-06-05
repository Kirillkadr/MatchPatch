### match
```cpp
...
#include <memory>

 #include <vector>
 
 >>> 
#include "base/functional/callback.h"

 ... 
```
### patch
```cpp
#include "components/printing/common/print.mojom.h"

```

### match
```cpp
...
 namespace 
 printing 
 { 
 >>> 
class MetafileSkia
 ... } ...  
```
### patch
```cpp
class PrintRenderFrameHelper;
using PrintRenderFrameHelper_BraveImpl = PrintRenderFrameHelper;

```

### match
```cpp
...
 
 namespace printing { ... 
 class PrepareFrameAndViewForPrint 
 ; 
 >>> 
// Stores reference to frame using WebVew and unique name.
 ... } ...  
```
### patch
```cpp
#define PrintRenderFrameHelper PrintRenderFrameHelper_ChromiumImpl

```

### match
```cpp
...
 
 namespace printing { ... 
 
 class PrintRenderFrameHelper
    : public blink::WebPrintClient,
      public content::RenderFrameObserver,
      public content::RenderFrameObserverTracker<PrintRenderFrameHelper>,
      public mojom::PrintRenderFrame { ... 
 
 class ScriptingThrottler { ... 
int count_ = 0;
 } 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  friend PrintRenderFrameHelper_BraveImpl;

```

### match
```cpp
...
 
 namespace printing { ... 
 
 class PrintRenderFrameHelper
    : public blink::WebPrintClient,
      public content::RenderFrameObserver,
      public content::RenderFrameObserverTracker<PrintRenderFrameHelper>,
      public mojom::PrintRenderFrame { ... 
#if BUILDFLAG(ENABLE_PRINT_PREVIEW)
  void PrintForSystemDialog() override;
  void SetPrintPreviewUI(
      mojo::PendingAssociatedRemote<mojom::PrintPreviewUI> preview) override;
  void InitiatePrintPreview(
#if BUILDFLAG(IS_CHROMEOS)
      mojo::PendingAssociatedRemote<mojom::PrintRenderer> print_renderer,
#endif
      bool has_selection) override;
  void PrintPreview(base::DictValue settings) override;
  void OnPrintPreviewDialogClosed() override;
#endif  // BUILDFLAG(ENABLE_PRINT_PREVIEW)
  void PrintFrameContent(mojom::PrintFrameContentParamsPtr params,
                         PrintFrameContentCallback callback) override;
  void PrintingDone(bool success) override;
  void ConnectToPdfRenderer() override;
  void PrintNodeUnderContextMenu() override;

  // Update |ignore_css_margins_| based on settings.
  void UpdateFrameMarginsCssInfo(const base::DictValue& settings);

#if BUILDFLAG(ENABLE_PRINT_PREVIEW)
  // Prepare frame for creating preview document.
  void PrepareFrameForPreviewDocument();

  // Continue creating preview document.
  void OnFramePreparedForPreviewDocument();

  // Initialize the print preview document.
  CreatePreviewDocumentResult CreatePreviewDocument();

  // Renders a print preview page. `page_index` is 0-based.
  // Returns true if print preview should continue, false on failure.
  bool RenderPreviewPage(uint32_t page_index,
                         blink::WebLocalFrame* header_footer_frame);

  // Finalize the print ready preview document.
  bool FinalizePrintReadyDocument();

#if BUILDFLAG(IS_CHROMEOS)
  // Called after a preview document has been created by a PrintRenderer.
  void OnPreviewDocumentCreated(
      int document_cookie,
      base::TimeTicks begin_time,
      base::ReadOnlySharedMemoryRegion preview_document_region);
#endif

  // Finish processing the preview document created by a PrintRenderer (record
  // the render time, update the PrintPreviewContext, and finalize the print
  // ready preview document).
  bool ProcessPreviewDocument(
      base::TimeTicks begin_time,
      base::ReadOnlySharedMemoryRegion preview_document_region);

  // Helper method to calculate the scale factor for fit-to-page.
  int GetFitToPageScaleFactor(const gfx::RectF& printable_area_in_points);
#endif  // BUILDFLAG(ENABLE_PRINT_PREVIEW)

  // Main printing code -------------------------------------------------------

  // Print with the system dialog.
  // WARNING: |this| may be gone after this method returns.
  void Print(blink::WebLocalFrame* frame,
             const blink::WebNode& node,
             PrintRequestType print_request_type);

  // Notification when printing is done - signal tear-down/free resources.
  void DidFinishPrinting(PrintingResult result);

  // Print Settings -----------------------------------------------------------

  // Initialize print page settings with default settings.
  // Used only for native printing workflow.
  bool InitPrintSettings(blink::WebLocalFrame* frame,
                         const blink::WebNode& node);

  // Calculate number of pages in source document.
  uint32_t CalculateNumberOfPages(blink::WebLocalFrame* frame,
                                  const blink::WebNode& node);

#if BUILDFLAG(ENABLE_PRINT_PREVIEW)
  // Set options for print preset from source PDF document.
  mojom::OptionsFromDocumentParamsPtr SetOptionsFromPdfDocument();

  // Update the current print settings with new `job_settings`.
  // `job_settings` contains print job details such as printer name, number of
  // copies, page range, etc.
  bool UpdatePrintSettings(blink::WebLocalFrame* frame,
                           const blink::WebNode& node,
                           const base::DictValue& job_settings);
#endif  // BUILDFLAG(ENABLE_PRINT_PREVIEW)

  // Returns final print settings from the user.
  // WARNING: |this| may be gone after this method returns.
  mojom::PrintPagesParamsPtr GetPrintSettingsFromUser(
      blink::WebLocalFrame* frame,
      const blink::WebNode& node,
      uint32_t expected_pages_count,
      PrintRequestType print_request_type);

  // Page Printing / Rendering ------------------------------------------------

  void OnFramePreparedForPrintPages();
  void PrintPages();
  bool PrintPagesNative(blink::WebLocalFrame* frame,
                        uint32_t page_count,
                        const std::vector<uint32_t>& pages_to_print);
  void FinishFramePrinting();
  // Render the frame for printing.
  bool RenderPagesForPrint(blink::WebLocalFrame* frame,
                           const blink::WebNode& node);

  // Helper function for rendering page at `page_index` to `metafile`.
  PrintPageInternalResult PrintPageInternal(
      const mojom::PrintParams& params,
      uint32_t page_index,
      uint32_t page_count,
      blink::WebLocalFrame* frame,
      blink::WebLocalFrame* header_footer_frame,
      MetafileSkia* metafile);

  // Helper methods -----------------------------------------------------------

  // Increments the IPC nesting level when an IPC message is received.
  void IPCReceived();

  // Decrements the IPC nesting level once an IPC message has been processed.
  void IPCProcessed();

  // Script Initiated Printing ------------------------------------------------

  // Return true if script initiated printing is currently
  // allowed. |user_initiated| should be true when a user event triggered the
  // script, most likely by pressing a print button on the page.
  bool IsScriptInitiatedPrintAllowed(blink::WebLocalFrame* frame,
                                     bool user_initiated);

#if BUILDFLAG(ENABLE_PRINT_PREVIEW)
  // Shows scripted print preview when options from plugin are available.
  void ShowScriptedPrintPreview();

  // WARNING: |this| may be gone after this method returns when |type| is
  // PRINT_PREVIEW_SCRIPTED.
  void RequestPrintPreview(PrintPreviewRequestType type,
                           bool already_notified_frame);

  // Checks whether print preview should continue or not.
  // Returns true if canceling, false if continuing.
  bool CheckForCancel();

  // Notifies the browser a print preview page has been rendered for modifiable
  // content.
  // `page_index` is 0-based.
  // `metafile` is the rendered page and should be valid.
  // Returns true if print preview should continue, false on failure.
  bool PreviewPageRendered(uint32_t page_index,
                           std::unique_ptr<MetafileSkia> metafile);

  // Called when the connection with the |preview_ui_| goes away.
  void OnPreviewDisconnect();
#endif  // BUILDFLAG(ENABLE_PRINT_PREVIEW)

  // `settings` must be valid.
  void SetPrintPagesParams(const mojom::PrintPagesParams& settings);

  // Quits active runloop waiting for Mojo reply. It's called when
  // |print_manager_host_| is disconnected before the replies.
  void QuitActiveRunLoop();

  // Quits a runloop waiting for a Mojo reply. These are called when a Mojo
  // message gets a reply.
  void QuitScriptedPrintPreviewRunLoop();

  // Resets internal state
  void Reset();

  // WebView used only to print the selection.
  std::unique_ptr<PrepareFrameAndViewForPrint> prep_frame_view_;
  bool reset_prep_frame_view_ = false;

  mojom::PrintPagesParamsPtr print_pages_params_;
  gfx::Rect printer_printable_area_;
  bool is_print_ready_metafile_sent_ = false;
  bool ignore_css_margins_ = false;

  // Let the browser process know of a printing failure. Only set to false when
  // the failure came from the browser in the first place.
  bool notify_browser_of_print_failure_ = true;

  // Used to check the prerendering status.
  const std::unique_ptr<Delegate> delegate_;

#if BUILDFLAG(IS_CHROMEOS)
  // Settings used by a PrintRenderer to create a preview document.
  base::DictValue print_renderer_job_settings_;

  // Used to render print documents from an external source (ARC, Crostini,
  // etc.).
  mojo::AssociatedRemote<mojom::PrintRenderer> print_renderer_;
#endif

#if BUILDFLAG(ENABLE_PRINT_PREVIEW)
  // Used to notify the browser of preview UI actions.
  mojo::AssociatedRemote<mojom::PrintPreviewUI> preview_ui_;
#endif

  mojo::AssociatedReceiverSet<mojom::PrintRenderFrame> receivers_;

  // Keeps track of the state of print preview between messages.
  // TODO(vitalybuka): Create PrintPreviewContext when needed and delete after
  // use. Now it's interaction with various messages is confusing.
  class PrintPreviewContext {
   public:
    PrintPreviewContext();
    PrintPreviewContext(const PrintPreviewContext&) = delete;
    PrintPreviewContext& operator=(const PrintPreviewContext&) = delete;
    ~PrintPreviewContext();

    // Initializes the print preview context. Need to be called to set
    // the |web_frame| / |web_node| to generate the print preview for.
    void InitWithFrame(blink::WebLocalFrame* web_frame);
    void InitWithNode(const blink::WebNode& web_node);

    // Dispatchs onbeforeprint/onafterprint events. Use these instead of calling
    // the WebLocalFrame version on source_frame().
    void DispatchBeforePrintEvent(
        base::WeakPtr<PrintRenderFrameHelper> weak_this);
    void DispatchAfterPrintEvent();

    // Does bookkeeping at the beginning of print preview.
    void OnPrintPreview();

    // Create the print preview document. |pages| is empty to print all pages.
    bool CreatePreviewDocument(
        std::unique_ptr<PrepareFrameAndViewForPrint> prepared_frame,
        const PageRanges& pages,
        mojom::SkiaDocumentType doc_type,
        int document_cookie,
        bool require_document_metafile);

    // Called after a page gets rendered. |page_time| is how long the
    // rendering took.
    void RenderedPreviewPage(base::TimeDelta page_time);

    // Called after a preview document gets rendered by a PrintRenderer.
    // |document_time| is how long the rendering took.
    void RenderedPreviewDocument(const base::TimeDelta document_time);

    // Updates the print preview context when the required pages are rendered.
    void AllPagesRendered();

    // Finalizes the print ready preview document.
    void FinalizePrintReadyDocument();

    // Cleanup after print preview finishes.
    void Finished();

    // Cleanup after print preview fails.
    void Failed(bool report_error);

    // Helper functions
    uint32_t GetNextPageIndex();
    bool IsRendering() const;
#if BUILDFLAG(IS_CHROMEOS)
    bool IsForArc() const;
#endif
    bool IsPlugin() const;
    bool IsModifiable() const;
    bool HasSelection();
    bool IsLastPageOfPrintReadyMetafile() const;
    bool IsFinalPageRendered() const;

    // Setters
#if BUILDFLAG(IS_CHROMEOS)
    void SetIsForArc(bool is_for_arc);
#endif
    void set_error(PrintPreviewErrorBuckets error);

    // Getters
    // Original frame for which preview was requested.
    blink::WebLocalFrame* source_frame();
    // Original node for which preview was requested.
    const blink::WebNode& source_node() const;

    // Frame to be use to render preview. May be the same as source_frame(), or
    // generated from it, e.g. copy of selected block.
    blink::WebLocalFrame* prepared_frame();
    // Node to be use to render preview. May be the same as source_node(), or
    // generated from it, e.g. copy of selected block.
    const blink::WebNode& prepared_node() const;

    uint32_t total_page_count() const;
    const std::vector<uint32_t>& pages_to_render() const;
    size_t pages_rendered_count() const;
    MetafileSkia* metafile();
    ContentProxySet* typeface_content_info();
    ContentProxySet* image_content_info();

   private:
    enum class State {
      kUninitialized,  // Not ready to render.
      kInitialized,    // Ready to render.
      kRendering,      // Rendering.
      kDone            // Finished rendering.
    };

    // Reset some of the internal rendering context.
    void ClearContext();

    void CalculatePluginAttributes();

    // Specifies what to render for print preview.
    FrameReference source_frame_;
    blink::WebNode source_node_;

    std::unique_ptr<PrepareFrameAndViewForPrint> prep_frame_view_;

    // The typefaces encountered in the content during document serialization.
    ContentProxySet typeface_content_info_;

    // The images encountered in the content during document serialization.
    ContentProxySet image_content_info_;

    // A document metafile is needed when not using the print compositor.
    std::unique_ptr<MetafileSkia> metafile_;

    // Total page count in the renderer.
    uint32_t total_page_count_ = 0;

    // The current page to render.
    int current_page_index_ = 0;

    // List of page indices that need to be rendered.
    std::vector<uint32_t> pages_to_render_;

    // True, if the document source is a plugin.
    bool is_plugin_ = false;

    // True, if the document source is modifiable. e.g. HTML and not PDF.
    bool is_modifiable_ = true;

#if BUILDFLAG(IS_CHROMEOS)
    // True, if the document source is from ARC.
    bool is_for_arc_ = false;
#endif

    // Specifies the total number of pages in the print ready metafile.
    int print_ready_metafile_page_count_ = 0;

    base::TimeDelta document_render_time_;
    base::TimeTicks begin_time_;

    PrintPreviewErrorBuckets error_ = PrintPreviewErrorBuckets::kNone;

    State state_ = State::kUninitialized;
  };

  class ScriptingThrottler {
   public:
    ScriptingThrottler();
    ScriptingThrottler(const ScriptingThrottler&) = delete;
    ScriptingThrottler& operator=(const ScriptingThrottler&) = delete;

    // Returns false if script initiated printing occurs too often.
    bool IsAllowed(blink::WebLocalFrame* frame);

    // Reset the counter for script initiated printing.
    // Scripted printing will be allowed to continue.
    void Reset();

   private:
    base::Time last_print_;
    int count_ = 0;
  };

    friend PrintRenderFrameHelper_BraveImpl;
		void SetupOnStopLoadingTimeout();
  void PrintRequestedPagesInternal(bool already_notified_frame);

  ScriptingThrottler scripting_throttler_;

  bool print_in_progress_ = false;
  PrintPreviewContext print_preview_context_;
  bool is_loading_ = false;
  bool is_scripted_preview_delayed_ = false;
  int ipc_nesting_level_ = 0;
  bool render_frame_gone_ = false;
  bool delete_pending_ = false;

  // If tagged PDF exporting is enabled, we also need to capture an
  // accessibility tree and store it in the metafile. AXTreeSnapshotter should
  // stay alive through the duration of printing one document, because text
  // drawing commands are only annotated with a DOMNodeId if accessibility
  // is enabled.
  std::unique_ptr<content::AXTreeSnapshotter> snapshotter_;

  // Used for two reasons:
  // * To give the document time to finish loading any pending resources that
  //   are desired for printing.
  // * To fix a race condition where the source is a PDF and print preview
  //   hangs because RequestPrintPreview is called before DidStopLoading() is
  //   called. This is a store for the RequestPrintPreview() call and its
  //   parameters so that it can be invoked after DidStopLoading.
  base::OnceClosure on_stop_loading_closure_;

  // This is used to report PrintWithParams() call result.
  PrintWithParamsCallback print_with_params_callback_;

  // Stores the quit closures of Mojo responses.
  scoped_refptr<ClosuresForMojoResponse> closures_for_mojo_responses_;

  bool do_deferred_print_for_system_dialog_ = false;

  mojo::AssociatedRemote<mojom::PrintManagerHost> print_manager_host_;

  // Stores a test-only callback for verifying the WebDocument values of the
  // preview document.
  PreviewDocumentTestCallback preview_document_test_callback_;

  base::WeakPtrFactory<PrintRenderFrameHelper> weak_ptr_factory_{this};
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
class PrintRenderFrameHelper : public PrintRenderFrameHelper_ChromiumImpl {
 public:
  PrintRenderFrameHelper(content::RenderFrame* render_frame,
                         std::unique_ptr<Delegate> delegate);
  PrintRenderFrameHelper(const PrintRenderFrameHelper&) = delete;
  PrintRenderFrameHelper& operator=(const PrintRenderFrameHelper&) = delete;
  ~PrintRenderFrameHelper() override;
 private:
  // printing::mojom::PrintRenderFrame:
#if BUILDFLAG(ENABLE_PRINT_PREVIEW)
  void SetPrintPreviewUI(
      mojo::PendingAssociatedRemote<mojom::PrintPreviewUI> preview) override;
  void InitiatePrintPreview(bool has_selection) override;
  void SetIsPrintPreviewExtraction(bool value) override;

  bool is_print_preview_extraction_ = false;
#endif
};

```

### match
```cpp
...
 
 namespace printing { ... 
 } 
 // namespace printing 
 >>> 
 ... 
```
### patch
```cpp
#undef PrintRenderFrameHelper

```

