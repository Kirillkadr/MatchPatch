### match
```
...
 
 # ifndef ...   >>> 
 class 
 DownloadItemModel 
 : 
 public 
 DownloadUIModel 
 ,  <<< 
public
 ...
```
### patch
```
class DownloadItemModel_Chromium : public DownloadUIModel,

```

### match
```
...
 
 # ifndef ... 
 
 class DownloadItemModel_Chromium : public DownloadUIModel,
public download::DownloadItem::Observer { ... 
// are desired by providing a StatusTextBuilderBase instance.  >>> 
 explicit DownloadItemModel(download::DownloadItem* download);  <<< 
DownloadItemModel(download::DownloadItem* download,
                    std::unique_ptr<DownloadUIModel::StatusTextBuilderBase>
                        status_text_builder);
 ... } ...
```
### patch
```
  explicit DownloadItemModel_Chromium(download::DownloadItem* download);

```

### match
```
...
   >>> 
 DownloadItemModel 
 ( 
 download::DownloadItem* download 
 ,  <<< 
std::unique_ptr<DownloadUIModel::StatusTextBuilderBase>
                        status_text_builder
 ... ) ...
```
### patch
```

  DownloadItemModel_Chromium(download::DownloadItem* download,

```

### match
```
...
 
 # ifndef ... 
 
 class DownloadItemModel_Chromium : public DownloadUIModel,
public download::DownloadItem::Observer { ... 
DownloadItemModel_Chromium(download::DownloadItem* download,
std::unique_ptr<DownloadUIModel::StatusTextBuilderBase>
                        status_text_builder);  >>> 
 DownloadItemModel(const DownloadItemModel&) = delete; 
 DownloadItemModel& operator=(const DownloadItemModel&) = delete;  <<< 
~DownloadItemModel() override;
 ... } ...  
```
### patch
```
  DownloadItemModel_Chromium(const DownloadItemModel_Chromium&) = delete;
  DownloadItemModel_Chromium& operator=(const DownloadItemModel_Chromium&) = delete;

```

### match
```
...
 
 # ifndef ... 
 
 class DownloadItemModel_Chromium : public DownloadUIModel,
public download::DownloadItem::Observer { ... 
DownloadItemModel_Chromium& operator=(const DownloadItemModel_Chromium&) = delete;  >>> 
 ~DownloadItemModel() override;  <<< 
// DownloadUIModel implementation.
 ... } ...  
```
### patch
```

  ~DownloadItemModel_Chromium() override;

```

### match
```
...
 
 # ifndef ... 
 
 class DownloadItemModel_Chromium : public DownloadUIModel,
public download::DownloadItem::Observer { ... 
raw_ptr<download::DownloadItem> download_;
 } 
 ; 
 >>> 
 ... 
```
### patch
```
class DownloadItemModel : public DownloadItemModel_Chromium {
 public:
  using DownloadItemModel_Chromium::DownloadItemModel_Chromium;
  ~DownloadItemModel() override = default;

  // Provides factory methods to create DownloadItemModel,
  // not DownloadItemModel_Chromium.
  static DownloadUIModelPtr Wrap(download::DownloadItem* download);
  static DownloadUIModelPtr Wrap(
      download::DownloadItem* download,
      std::unique_ptr<DownloadUIModel::StatusTextBuilderBase>
          status_text_builder);

  // Deletes the local file associated with this download.
  void DeleteLocalFile() override;
  void CopyDownloadLinkToClipboard() override;
#if !BUILDFLAG(IS_ANDROID)
  bool IsCommandEnabled(const DownloadCommands* download_commands,
                        DownloadCommands::Command command) const override;
  void ExecuteCommand(DownloadCommands* download_commands,
                      DownloadCommands::Command command) override;
#endif  // !BUILDFLAG(IS_ANDROID)
};


```

