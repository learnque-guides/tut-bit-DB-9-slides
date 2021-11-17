# Batch read, update for speedup

Sometimes you must perform DML processes (select, update, delete or combinations of these) on large SQL Server tables.

## Basic algorithm

```sql
DECLARE @id_control INT
DECLARE @batchSize INT
DECLARE @results INT

SET @results = 1 --stores the row count after each successful batch
SET @batchSize = 10000 --How many rows you want to operate on each batch
SET @id_control = 0 --current batch 

-- when 0 rows returned, exit the loop
WHILE (@results > 0) 
BEGIN
   -- put your custom code here
   SELECT * -- OR DELETE OR UPDATE
   FROM <any Table>
   WHERE <your logic evaluations>
   (
      AND <your PK> > @id_control
      AND <your PK> <= @id_control + @batchSize
   )
   -- very important to obtain the latest rowcount to avoid infinite loops
   SET @results = @@ROWCOUNT

   -- next batch
   SET @id_control = @id_control + @batchSize
END
```
