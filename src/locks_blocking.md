# Locks and blocking

* By default, a SQL Server uses a pure locking model to enforce the isolation property of transactions.
* Azure SQL Database uses the row-versioning model by default.
* Locks are control resources obtained by a transaction to guard data resources, preventing conflicting or incompatible access by other transactions.
* Exclusive locks are called "exclusive" because you cannot obtain an exclusive lock on a resource if another transaction is holding any lock mode on the resource.
* Shared locks - When you try to read data, by default your transaction requests a shared lock on the data resource and releases the lock as soon as the read statement is done with that resource. This lock mode is called "shared" because multiple transactions can hold shared locks on the same data resource simultaneously. In this case we can have two types of isolation:
    * READ COMMITTED - you can read data after write operation is done (pesimistic concurrency);
    * READ COMMITTED SNAPSHOT - you can read latest data that was written to table (optimistic concurrency);
