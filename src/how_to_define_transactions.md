# How to define transaction

* You can define transaction boundaries either explicitly or implicitly.
* You define the beginning of a transaction explicitly with a BEGIN TRAN (or BEGIN TRANSACTION) statement. 
* You define the end of a transaction explicitly with a COMMIT TRAN statement if you want to commit it and with a ROLLBACK TRAN (or ROLLBACK TRANSACTION) statement if you want to undo its changes.

```sql
BEGIN TRAN;
  INSERT INTO dbo.T1(keycol, col1, col2) VALUES(4, 101, 'C');
  INSERT INTO dbo.T2(keycol, col1, col2) VALUES(4, 201, 'X');
COMMIT TRAN;
```

* If you do not mark the boundaries of a transaction explicitly, by default, SQL Server treats each individual statement as a transaction; in other words, by default, SQL Server automatically commits the transaction at the end of each statement.
* You can change the way SQL Server handles implicit transactions with a session option called IMPLICIT_TRANSACTIONS.

```sql
ALTER DATABASE lessons SET IMPLICIT_TRANSACTIONS OFF;
```