# Transaction and ACID

Transactions have four properties—atomicity, consistency, isolation, and durability—abbreviated with the acronym ACID:

* *Atomicity* - A transaction is an atomic unit of work. Either all changes in the transaction take place or none do. If the system fails before a transaction is completed (before the commit instruction is recorded in the transaction log), upon restart, SQL Server undoes the changes that took place.

Note: Some errors, such as primary-key violations and lock-expiration timeouts, are not considered severe enough to justify an automatic rollback of the transaction. You need to handle such exception by yourself and explicitly rollback changes

* *Consistency* - the term consistency refers to the state of the data that the relational database management system (RDBMS) gives you access to as concurrent transactions modify and query it. 

* *Isolation* - ensures that transactions access only consistent data. Depends on isolation levels. The easiest mechanizm is data locking.

* *Durability* - data changes are always written to the database’s transaction log on disk before they are written to the data portion of the database on disk.