### match
```cpp
...
 
 namespace history { ... 
 
 namespace { ... 
TEST_F(HistoryDeleteDirectiveHandlerTest, ProcessUrlDeleteDirective) {
  const GURL test_url1("http://www.google.com/");
  const GURL test_url2("http://maps.google.com/");

  AddPage(test_url1, UnixUsecToTime(3));
  AddPage(test_url2, UnixUsecToTime(6));
  AddPage(test_url1, UnixUsecToTime(10));

  {
    QueryURLAndVisitsResult query = QueryURLAndVisits(test_url1);
    EXPECT_TRUE(query.success);
    ASSERT_EQ(2, query.row.visit_count());
    EXPECT_TRUE(QueryURLAndVisits(test_url2).success);
  }

  // Delete the first visit of url1 and all visits of url2.
  syncer::SyncDataList directives;
  sync_pb::EntitySpecifics entity_specs1;
  sync_pb::UrlDirective* url_directive =
      entity_specs1.mutable_history_delete_directive()->mutable_url_directive();
  url_directive->set_url(test_url1.spec());
  url_directive->set_end_time_usec(8);
  directives.push_back(
      syncer::SyncData::CreateRemoteData(entity_specs1, kFakeClientTagHash));
  sync_pb::EntitySpecifics entity_specs2;
  url_directive =
      entity_specs2.mutable_history_delete_directive()->mutable_url_directive();
  url_directive->set_url(test_url2.spec());
  url_directive->set_end_time_usec(8);
  directives.push_back(
      syncer::SyncData::CreateRemoteData(entity_specs2, kFakeClientTagHash));

  syncer::FakeSyncChangeProcessor change_processor;
  EXPECT_FALSE(handler()
                   ->MergeDataAndStartSyncing(
                       syncer::HISTORY_DELETE_DIRECTIVES, directives,
                       std::unique_ptr<syncer::SyncChangeProcessor>(
                           new syncer::SyncChangeProcessorWrapperForTest(
                               &change_processor)))
                   .has_value());

  // Inject a task to check status and keep message loop filled before
  // directive processing finishes.
  base::SingleThreadTaskRunner::GetCurrentDefault()->PostTask(
      FROM_HERE, base::BindOnce(&CheckDirectiveProcessingResult,
                                base::Time::Now() + base::Seconds(10),
                                &change_processor, 2));
  base::RunLoop().RunUntilIdle();

  QueryURLAndVisitsResult query = QueryURLAndVisits(test_url1);
  EXPECT_TRUE(query.success);
  EXPECT_EQ(UnixUsecToTime(10), query.visits[0].visit_time);
  EXPECT_FALSE(QueryURLAndVisits(test_url2).success);

  // Expect a sync change for deleting processed directives.
  const syncer::SyncChangeList& sync_changes = change_processor.changes();
  ASSERT_EQ(2u, sync_changes.size());
  EXPECT_EQ(syncer::SyncChange::ACTION_DELETE, sync_changes[0].change_type());
  EXPECT_EQ(syncer::SyncChange::ACTION_DELETE, sync_changes[1].change_type());
}
 } 
 // namespace 
 >>> 
 ... } ...  
```
### patch
```cpp
namespace {
TEST_F(HistoryDeleteDirectiveHandlerTest,
       BraveCreateUrlDeleteDirectiveReturnsFalse) {
  EXPECT_FALSE(handler()->CreateUrlDeleteDirective(GURL("https://brave.com")));
}

}  // namespace

```

