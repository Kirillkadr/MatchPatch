### match
```cpp
...
 
 namespace { ...   >>> 
 int 
 GetCommandIdInt(SplitTabMenuModel::CommandId command_id) 
 {  <<< 
// Start command IDs at 1701 to avoid conflicts with other submenus.
 ... } ...  } ...  
```
### patch
```cpp
int GetCommandIdInt_Chromium(SplitTabMenuModel::CommandId command_id) {

```

### match
```cpp
...
 
 namespace { ...   >>> 
 SplitTabMenuModel::CommandId 
 GetCommandIdEnum(int command_id) 
 {  <<< 
return static_cast<SplitTabMenuModel::CommandId>(
      command_id - ExistingBaseSubMenuModel::kMinSplitTabMenuModelCommandId);
 ... } ...  } ...  
```
### patch
```cpp
SplitTabMenuModel::CommandId GetCommandIdEnum_Chromium(int command_id) {

```

### match
```cpp
...
 
 namespace { ... 
 
 std::string_view GetMetricsSuffixForCommand(
    SplitTabMenuModel::CommandId command_id) { ... 
 
 case SplitTabMenuModel : ... 
 return "SendFeedback"; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
    case CommandId::kToggleLinkState: {
        split_tab_data->set_linked(!split_tab_data->linked());
        break;
    }

```

### match
```cpp
...
>>>
 GetCommandIdInt(CommandId::kExitSplit) 
 , 
 IDS_SPLIT_TAB_SEPARATE_VIEWS 
 ,  <<< 
ui::ImageModel::FromVectorIcon(kOpenInFullIcon, ui::kColorMenuIcon,
                                     ui::SimpleMenuModel::kDefaultIconSize)
 ... 
```
### patch
```cpp
      GetCommandIdInt_Chromium(CommandId::kExitSplit), IDS_SPLIT_TAB_SEPARATE_VIEWS,

```

### match
```cpp
...
 
 if (menu_source == MenuSource::kMiniToolbar) { ...   >>> 
 GetCommandIdInt(CommandId::kCloseSpecifiedTab) 
 , 
 IDS_SPLIT_TAB_CLOSE 
 ,  <<< 
ui::ImageModel::FromVectorIcon(vector_icons::kCloseChromeRefreshIcon,
                                       ui::kColorMenuIcon,
                                       ui::SimpleMenuModel::kDefaultIconSize)
 ... } ...  
```
### patch
```cpp
        GetCommandIdInt_Chromium(CommandId::kCloseSpecifiedTab), IDS_SPLIT_TAB_CLOSE,

```

### match
```cpp
...
 
 if (menu_source == MenuSource::kMiniToolbar) { ... 
 
 SetElementIdentifierAt ( ...   >>> 
 GetIndexOfCommandId(GetCommandIdInt(CommandId::kCloseSpecifiedTab))  <<<  ...) ...  } ...  
```
### patch
```cpp
        GetIndexOfCommandId(GetCommandIdInt_Chromium(CommandId::kCloseSpecifiedTab))

```

### match
```cpp
...
 
 SplitTabMenuModel::SplitTabMenuModel(TabStripModel* tab_strip_model,
                                     MenuSource menu_source,
                                     std::optional<int> split_tab_index)
    : ui::SimpleMenuModel(this),
      tab_strip_model_(tab_strip_model),
      menu_source_(menu_source),
      split_tab_index_(split_tab_index) { ... 
 
 if (menu_source == MenuSource::kTabContextMenu ||
             menu_source == MenuSource::kToolbarButton) { ...   >>> 
 AddItem(GetCommandIdInt(CommandId::kCloseStartTab), std::u16string()); 
 AddItem(GetCommandIdInt(CommandId::kCloseEndTab), std::u16string());  <<< 
AddSeparator(ui::MenuSeparatorType::NORMAL_SEPARATOR);
 ... } ...  } ...  
```
### patch
```cpp
    AddItem(GetCommandIdInt_Chromium(CommandId::kCloseStartTab), std::u16string());
    AddItem(GetCommandIdInt_Chromium(CommandId::kCloseEndTab), std::u16string());

```

### match
```cpp
...
 
 SplitTabMenuModel::SplitTabMenuModel(TabStripModel* tab_strip_model,
                                     MenuSource menu_source,
                                     std::optional<int> split_tab_index)
    : ui::SimpleMenuModel(this),
      tab_strip_model_(tab_strip_model),
      menu_source_(menu_source),
      split_tab_index_(split_tab_index) { ... 
 
 if (menu_source == MenuSource::kTabContextMenu ||
             menu_source == MenuSource::kToolbarButton) { ... 
 
 SetElementIdentifierAt ( ...   >>> 
 GetIndexOfCommandId(GetCommandIdInt(CommandId::kCloseStartTab)).value() 
 ,  <<<  ...) ...  } ...  } ...  
```
### patch
```cpp
        GetIndexOfCommandId(GetCommandIdInt_Chromium(CommandId::kCloseStartTab)).value(),

```

### match
```cpp
...
 
 SplitTabMenuModel::SplitTabMenuModel(TabStripModel* tab_strip_model,
                                     MenuSource menu_source,
                                     std::optional<int> split_tab_index)
    : ui::SimpleMenuModel(this),
      tab_strip_model_(tab_strip_model),
      menu_source_(menu_source),
      split_tab_index_(split_tab_index) { ... 
 
 if (menu_source == MenuSource::kTabContextMenu ||
             menu_source == MenuSource::kToolbarButton) { ... 
 
 SetElementIdentifierAt ( ...   >>> 
 GetIndexOfCommandId(GetCommandIdInt(CommandId::kCloseEndTab)).value() 
 ,  <<<  ...) ...  } ...  } ...  
```
### patch
```cpp
        GetIndexOfCommandId(GetCommandIdInt_Chromium(CommandId::kCloseEndTab)).value(),

```

### match
```cpp
...
 
 SplitTabMenuModel::SplitTabMenuModel(TabStripModel* tab_strip_model,
                                     MenuSource menu_source,
                                     std::optional<int> split_tab_index)
    : ui::SimpleMenuModel(this),
      tab_strip_model_(tab_strip_model),
      menu_source_(menu_source),
      split_tab_index_(split_tab_index) { ... 
if (menu_source == MenuSource::kMiniToolbar) {
    CHECK(split_tab_index.has_value());
    AddItemWithStringIdAndIcon(
                GetCommandIdInt_Chromium(CommandId::kCloseSpecifiedTab), IDS_SPLIT_TAB_CLOSE,
		ui::ImageModel::FromVectorIcon(vector_icons::kCloseChromeRefreshIcon,
                                       ui::kColorMenuIcon,
                                       ui::SimpleMenuModel::kDefaultIconSize));
    SetElementIdentifierAt(
                GetIndexOfCommandId(GetCommandIdInt_Chromium(CommandId::kCloseSpecifiedTab))
			.value(),
        kCloseMenuItem);
  } else if (menu_source == MenuSource::kTabContextMenu ||
             menu_source == MenuSource::kToolbarButton) {
        AddItem(GetCommandIdInt_Chromium(CommandId::kCloseStartTab), std::u16string());
		    AddItem(GetCommandIdInt_Chromium(CommandId::kCloseEndTab), std::u16string());
		AddSeparator(ui::MenuSeparatorType::NORMAL_SEPARATOR);

    SetElementIdentifierAt(
                GetIndexOfCommandId(GetCommandIdInt_Chromium(CommandId::kCloseStartTab)).value(),
			kCloseStartTabMenuItem);
    SetElementIdentifierAt(
                GetIndexOfCommandId(GetCommandIdInt_Chromium(CommandId::kCloseEndTab)).value(),
			kCloseEndTabMenuItem);
  } else {
    NOTREACHED() << "Unknown close menu item option";
  }  >>> 
 AddItem(GetCommandIdInt(CommandId::kReversePosition), std::u16string());  <<< 
SetElementIdentifierAt(
      GetIndexOfCommandId(GetCommandIdInt(CommandId::kReversePosition)).value(),
      kReversePositionMenuItem);
 ... } ...  
```
### patch
```cpp
  AddItem(GetCommandIdInt_Chromium(CommandId::kReversePosition), std::u16string());

```

### match
```cpp
...
 
 SplitTabMenuModel::SplitTabMenuModel(TabStripModel* tab_strip_model,
                                     MenuSource menu_source,
                                     std::optional<int> split_tab_index)
    : ui::SimpleMenuModel(this),
      tab_strip_model_(tab_strip_model),
      menu_source_(menu_source),
      split_tab_index_(split_tab_index) { ... 
 
 SetElementIdentifierAt ( ...   >>> 
 GetIndexOfCommandId(GetCommandIdInt(CommandId::kReversePosition)).value() 
 ,  <<<  ...) ...  } ...  
```
### patch
```cpp
      GetIndexOfCommandId(GetCommandIdInt_Chromium(CommandId::kReversePosition)).value(),

```

### match
```cpp
...
 
 SplitTabMenuModel::SplitTabMenuModel(TabStripModel* tab_strip_model,
                                     MenuSource menu_source,
                                     std::optional<int> split_tab_index)
    : ui::SimpleMenuModel(this),
      tab_strip_model_(tab_strip_model),
      menu_source_(menu_source),
      split_tab_index_(split_tab_index) { ... 
 
 SetElementIdentifierAt ( ...   >>> 
 GetIndexOfCommandId(GetCommandIdInt(CommandId::kExitSplit)).value() 
 ,  <<<  ...) ...  } ...  
```
### patch
```cpp
      GetIndexOfCommandId(GetCommandIdInt_Chromium(CommandId::kExitSplit)).value(),

```

### match
```cpp
...
 
 if (menu_source == MenuSource::kToolbarButton &&
      chrome::CanShowFeedback(tab_strip_model->profile())) { ...   >>> 
 AddItemWithStringIdAndIcon 
 ( 
 GetCommandIdInt(CommandId::kSendFeedback) 
 ,  <<<  ...) ...  } ...  
```
### patch
```cpp
    AddItemWithStringIdAndIcon(GetCommandIdInt_Chromium(CommandId::kSendFeedback),

```

### match
```cpp
...
 
 bool SplitTabMenuModel::IsItemForCommandIdDynamic(int command_id) const { ...   >>> 
 const CommandId id = GetCommandIdEnum(command_id);  <<< 
return id == CommandId::kReversePosition || id == CommandId::kCloseStartTab ||
         id == CommandId::kCloseEndTab;
 ... } ...  
```
### patch
```cpp
  const CommandId id = GetCommandIdEnum_Chromium(command_id);

```

### match
```cpp
...
 
 std::u16string SplitTabMenuModel::GetLabelForCommandId(int command_id) const { ...   >>> 
 const CommandId id = GetCommandIdEnum(command_id);  <<< 
if (id == CommandId::kReversePosition) {
    return l10n_util::GetStringUTF16(IDS_SPLIT_TAB_REVERSE_VIEWS);
  } else if (id == CommandId::kCloseStartTab) {
    return l10n_util::GetStringUTF16(
        GetSplitLayout() == split_tabs::SplitTabLayout::kVertical
            ? IDS_SPLIT_TAB_CLOSE_LEFT_VIEW
            : IDS_SPLIT_TAB_CLOSE_TOP_VIEW);
  } else if (id == CommandId::kCloseEndTab) {
    return l10n_util::GetStringUTF16(
        GetSplitLayout() == split_tabs::SplitTabLayout::kVertical
            ? IDS_SPLIT_TAB_CLOSE_RIGHT_VIEW
            : IDS_SPLIT_TAB_CLOSE_BOTTOM_VIEW);
  } else {
    NOTREACHED() << "There are no other commands that are dynamic so this case "
                    "should not be reached.";
  }
 ... } ...  
```
### patch
```cpp
  const CommandId id = GetCommandIdEnum_Chromium(command_id);

```

### match
```cpp
...
 
 ui::ImageModel SplitTabMenuModel::GetIconForCommandId(int command_id) const { ... 
const split_tabs::SplitTabActiveLocation active_split_tab_location =
      split_tabs::GetLastActiveTabLocation(tab_strip_model_, GetSplitTabId());  >>> 
 const CommandId id = GetCommandIdEnum(command_id);  <<< 
const gfx::VectorIcon* icon = nullptr;
 ... } ...  
```
### patch
```cpp
  const CommandId id = GetCommandIdEnum_Chromium(command_id);

```

### match
```cpp
...
 
 void SplitTabMenuModel::ExecuteCommand(int command_id, int event_flags) { ... 
CHECK_EQ(tabs_in_split.size(), 2U);  >>> 
 CommandId split_command_id = GetCommandIdEnum(command_id);  <<< 
switch (split_command_id) {
    case CommandId::kReversePosition:
      tab_strip_model_->ReverseTabsInSplit(split_id);
      break;
    case CommandId::kCloseSpecifiedTab:
      CloseTabAtIndex(split_tab_index_.value());
      break;
    case CommandId::kCloseStartTab: {
      int startIndex = base::i18n::IsRTL() ? 1 : 0;
      CloseTabAtIndex(
          tab_strip_model_->GetIndexOfTab(tabs_in_split[startIndex]));
      break;
    }
    case CommandId::kCloseEndTab: {
      int endIndex = base::i18n::IsRTL() ? 0 : 1;
      CloseTabAtIndex(tab_strip_model_->GetIndexOfTab(tabs_in_split[endIndex]));
      break;
    }
    case CommandId::kExitSplit:
      tab_strip_model_->RemoveSplit(split_id);
      break;
    case CommandId::kSendFeedback:
      SendFeedback();
      break;
  }
 ... } ...  
```
### patch
```cpp
  CommandId split_command_id = GetCommandIdEnum_Chromium(command_id);

```

### match
```cpp
...
 
 void SplitTabMenuModel::ExecuteCommand(int command_id, int event_flags) { ... 
 
 case CommandId : ... 
SendFeedback();
 break; 
 >>> 
 ... } ...  
```
### patch
```cpp
    case CommandId::kToggleLinkState: {
        split_tab_data->set_linked(!split_tab_data->linked());
        break;
    }

```

### match
```cpp
...
 
 void SplitTabMenuModel::SendFeedback() { ... 
chrome::ShowFeedbackPage(browser, feedback::kFeedbackSourceSplitView, "", "",
                           "split_view", "");
 } 
 >>> 
 ... 
```
### patch
```cpp
// static
SplitTabMenuModel::CommandId SplitTabMenuModel::GetCommandIdEnum(
    int command_id) {
  return GetCommandIdEnum_Chromium(command_id);
}

// static
int SplitTabMenuModel::GetCommandIdInt(
    SplitTabMenuModel::CommandId command_id) {
  return GetCommandIdInt_Chromium(command_id);
}

```

