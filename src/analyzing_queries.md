# Analyzing queries

During execution of queries SQL server use such steps:

* Parsing — In the parsing phase, the query processor simply ensures that the query meets syntactic requirements.
* Resolution — In the resolution phase, the query processor ensures that all the object names specified in the query actually exist and are accessible.
* Optimization — During the optimization phase, the query processor evaluates a number of possible execution plans to determine which plan would cost the least. It will evaluate whether a single-processor or multiple-processor query would be the most efficient, as well as whether to use any existing indexes or column statistics. The query processor will not always choose the fastest plan. Sometimes it chooses a slower query plan because it costs less as far as CPU expenditures.
* Compilation — The optimized query plan is then compiled into a small executable during the compilation phase.
* Caching — This compiled plan is placed in cache during the caching phase.
* Execution — The compiled plan is executed during the execution phase.

During analyzing queries we need to disable two types of cache:

* The buffer cache and.
* The procedure cache.

```sql
-- Buffer cache
DBCC DROPCLEANBUFFERS
```

```sql
-- Procedure cache
DBCC FREEPROCCACHE
```

Sometimes it also usefull to run sp_recompile for stored procedure:

```sql
sp_recompile 'dbo.someProcedure';
```

SQL Server provides several session options that you can use to return information about the query being executed:

* STATISTICS IO - Returns the number of read and scan operations required to run the query.
* STATISTICS TIME - Returns the number of milliseconds required to parse, compile, and execute a query.
* STATISTICS PROFILE - Returns a textual showplan and query statistics.
* STATISTICS XML - Returns an XML document that contains a query plan and query statistics.
* SHOWPLAN_TEXT - Returns an estimated textual showplan. Does not actually run the query.
* SHOWPLAN_ALL - Returns an estimated textual showplan and query statistics. Does not actually run the query.
* SHOWPLAN_XML - Returns an XML document that contains an estimated query plan and query statistics. Does not actually run the query.
