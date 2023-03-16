#  ❔ DuckDB Metadata

Project to show the extent of database metadata provided by the [DuckDB JDBC driver](https://duckdb.org/docs/api/java.html).

# 🎯 Why ?

ONce metadata will be properly implemented, we'll be able to generate schemacrawler doc for
**`duckdb` database (which is actually not the case).**


# 🧪 Test

![image](https://user-images.githubusercontent.com/5235127/225747165-093d33c9-74a4-41c3-b268-9bac2e201b58.png)



```shell
gh repo clone sualeh/duckdb_metadata 
cd duckdb_metadata
mvn surefire-report:report
xdg-open target/site/surefire-report.html

```

which leads to lack of `getTypeInfo` (`java.sql.SQLFeatureNotSupportedException: getTypeInfo`)

`org.duckdb.DuckDBDatabaseMetaData.getTypeInfo(DuckDBDatabaseMetaData.java:953)`:

```
	
schemacrawler.schemacrawler.exceptions.ExecutionRuntimeException: getTypeInfo
	at schemacrawler.crawl.SchemaCrawler.crawl(SchemaCrawler.java:160)
	at schemacrawler.tools.catalogloader.SchemaCrawlerCatalogLoader.loadCatalog(SchemaCrawlerCatalogLoader.java:51)
	at schemacrawler.tools.catalogloader.ChainedCatalogLoader.loadCatalog(ChainedCatalogLoader.java:76)
	at schemacrawler.tools.utility.SchemaCrawlerUtility.getCatalog(SchemaCrawlerUtility.java:110)
	at schemacrawler.tools.executable.SchemaCrawlerExecutable.loadCatalog(SchemaCrawlerExecutable.java:181)
	at schemacrawler.tools.executable.SchemaCrawlerExecutable.execute(SchemaCrawlerExecutable.java:102)
	at schemacrawler.test.utility.ExecutableTestUtility.executableExecution(ExecutableTestUtility.java:75)
	at schemacrawler.test.utility.ExecutableTestUtility.executableExecution(ExecutableTestUtility.java:50)
	at us.fatehi.duckdb_metadata.DuckDBTest.testDuckDBWithConnection(DuckDBTest.java:82)
Caused by: java.sql.SQLFeatureNotSupportedException: getTypeInfo
	at org.duckdb.DuckDBDatabaseMetaData.getTypeInfo(DuckDBDatabaseMetaData.java:953)
	at org.apache.commons.dbcp2.DelegatingDatabaseMetaData.getTypeInfo(DelegatingDatabaseMetaData.java:933)
	at org.apache.commons.dbcp2.DelegatingDatabaseMetaData.getTypeInfo(DelegatingDatabaseMetaData.java:933)
	at schemacrawler.crawl.DataTypeRetriever.retrieveSystemColumnDataTypesFromMetadata(DataTypeRetriever.java:183)
	at schemacrawler.crawl.DataTypeRetriever.retrieveSystemColumnDataTypes(DataTypeRetriever.java:85)
	at us.fatehi.utility.scheduler.TimedTask.call(TimedTask.java:67)
	at us.fatehi.utility.scheduler.TimedTask.call(TimedTask.java:44)
	at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:264)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1136)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:635)
	at java.base/java.lang.Thread.run(Thread.java:833)
  ```
