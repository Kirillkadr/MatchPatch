### match
```
...
 
 namespace importer { ... 
 
 void LogImporterUseToMetrics(const std::string& metric_postfix,
                             user_data_importer::ImporterType type) { ... 
case user_data_importer::TYPE_EDGE:
      metrics_type = IMPORTER_METRICS_EDGE;
      break;
 #endif 
 >>> 
 ... } ...  } ...  
```
### patch
```
    case user_data_importer::TYPE_CHROME:
    case user_data_importer::TYPE_EDGE_CHROMIUM:
    case user_data_importer::TYPE_VIVALDI:
    case user_data_importer::TYPE_OPERA:
    case user_data_importer::TYPE_YANDEX:
    case user_data_importer::TYPE_WHALE:
    break;

```

