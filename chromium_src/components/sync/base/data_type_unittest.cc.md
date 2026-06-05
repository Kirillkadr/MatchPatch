### match
```cpp
...
 
 namespace syncer { ... 
 
 namespace { ... 
 
 TEST(DataTypeTest, DataTypeSetFromSpecificsFieldNumberList) { ... 
EXPECT_EQ(GetDataTypeSetFromSpecificsFieldNumberList(field_numbers),
            ProtocolTypes());
 } 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
TEST(DataTypeTest, EncryptableUserTypes) {
  EXPECT_TRUE(EncryptableUserTypes().Has(DEVICE_INFO));
  EXPECT_TRUE(EncryptableUserTypes().Has(HISTORY));
}
TEST(DataTypeTest, LowPriorityUserTypes) {
  EXPECT_TRUE(LowPriorityUserTypes().Has(HISTORY_DELETE_DIRECTIVES));
  EXPECT_FALSE(LowPriorityUserTypes().Has(HISTORY));
  EXPECT_TRUE(LowPriorityUserTypes().Has(USER_EVENTS));
}

// This test is supposed to fail when sync types are increased/decreased
TEST(DataTypeTest, DataTypeCounts) {
  EXPECT_EQ(static_cast<int>(DataTypeForHistograms::kMaxValue), 76);
}

```

