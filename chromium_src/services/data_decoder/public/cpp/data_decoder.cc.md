### match
```cpp
...
 
 namespace data_decoder { ... 
 
 void DataDecoder::ParseJson(const std::string& json,
                            ValueParseCallback callback) { ...   >>> 
 base::JSONReader::ReadAndReturnValueWithError(json, base::JSON_PARSE_RFC) 
 ;  <<<  ...} ...  } ...  
```
### patch
```cpp
      base::JSONReader::ReadAndReturnValueWithError(json, base::JSON_PARSE_RFC | base::JSON_ALLOW_TRAILING_COMMAS);

```

