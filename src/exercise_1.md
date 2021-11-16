# Exercise 1

* Open three connections in Azure Data Studio or SQL Server Management Studio. (The exercises will refer to them as Connection 1, Connection 2, and Connection 3.) Run the following code in Connection 1 to update rows in Sales.OrderDetails:

```sql
BEGIN TRAN;

  UPDATE Sales.OrderDetails
    SET discount = 0.05
  WHERE orderid = 10249;
```

* Run the following code in Connection 2 to query Sales.OrderDetails; Connection 2 will be blocked:

```sql
SELECT orderid, productid, unitprice, qty, discount
FROM Sales.OrderDetails
WHERE orderid = 10249;
```

* Run the following code in Connection 3, and identify the locks and session IDs involved in the blocking chain:

```sql
SELECT
    request_session_id            AS sid,
    resource_type                 AS restype,
    resource_database_id          AS dbid,
    resource_description          AS res,
    resource_associated_entity_id AS resid,
    request_mode                  AS mode,
    request_status                AS status
FROM sys.dm_tran_locks;
```

* Replace the session IDs `<ID1, ID2>` with the ones you found to be involved in the blocking chain in the previous exercise. Run the following code to obtain connection, session, and blocking information about the processes involved in the blocking chain:

```sql
-- Connection info:
SELECT -- use * to explore
    session_id AS sid,
    connect_time,
    last_read,
    last_write,
    most_recent_sql_handle
FROM sys.dm_exec_connections
WHERE session_id IN(<IDs>);

-- Session info
SELECT -- use * to explore
    session_id AS sid,
    login_time,
    host_name,
    program_name,
    login_name,
    nt_user_name,
    last_request_start_time,
    last_request_end_time
    FROM sys.dm_exec_sessions
WHERE session_id IN(<IDs>);

-- Blocking
SELECT -- use * to explore
    session_id AS sid,
    blocking_session_id,
    command,
    sql_handle,
    database_id,
    wait_type,
    wait_time,
    wait_resource
FROM sys.dm_exec_requests
WHERE blocking_session_id > 0;
```

* Run the following code in Connection 1 to roll back the transaction:

```sql
ROLLBACK TRAN;
```

Observe in Connection 2 that the SELECT query returned the two order detail rows, and that those rows were not modified.

Remember that if you need to terminate the blocker’s transaction, you can use the KILL command. Close all connections.