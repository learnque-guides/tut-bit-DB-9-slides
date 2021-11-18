# How to create a database with schemas?

```sql
USE master;

-- Drop database
IF DB_ID(N'some_database') IS NOT NULL DROP DATABASE some_database;

-- If database could not be created due to open connections, abort
IF @@ERROR = 3702 
   RAISERROR(N'Database cannot be dropped because there are still open connections.', 127, 127) WITH NOWAIT, LOG;

-- Create database
CREATE DATABASE some_database;
GO

USE some_database;
GO

CREATE SCHEMA some_schema AUTHORIZATION dbo;
GO

DROP TABLE IF EXISTS some_table;
GO

CREATE TABLE some_schema.some_table
(
    id INT NOT NULL IDENTITY PRIMAR KEY
);
GO
```

