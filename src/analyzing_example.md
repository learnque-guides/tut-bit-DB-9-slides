# Analyzing example

Let's create table:

```sql
USE [lessons]
GO
DROP TABLE IF EXISTS [MyOrders];

CREATE TABLE [MyOrders](
	[orderid] [int] NOT NULL,
	[custid] [int] NULL,
	[empid] [int] NOT NULL,
	[orderdate] [date] NOT NULL,
	[requireddate] [date] NOT NULL,
	[shippeddate] [date] NULL,
	[shipperid] [int] NOT NULL,
	[freight] [money] NOT NULL,
	[shipname] [nvarchar](40) NOT NULL,
	[shipaddress] [nvarchar](60) NOT NULL,
	[shipcity] [nvarchar](15) NOT NULL,
	[shipregion] [nvarchar](15) NULL,
	[shippostalcode] [nvarchar](10) NULL,
	[shipcountry] [nvarchar](15) NOT NULL,	
);
GO
```

Let's populate it with contact data:

```sql
INSERT INTO [MyOrders] SELECT * FROM [Sales].[Orders];
GO 10;
```

Execute query with statistic:

```sql
DBCC DROPCLEANBUFFERS;
DBCC FREEPROCCACHE;
SET STATISTICS IO ON;
GO
USE lessons;
GO
SELECT orderid, empid
FROM [MyOrders]
WHERE [shipaddress] = '7890 Milton Dr.';
GO
SET STATISTICS IO OFF;
GO
```

Execute another query with statistic:

```sql
DBCC DROPCLEANBUFFERS;
DBCC FREEPROCCACHE;
SET STATISTICS IO ON;
GO
USE lessons;
GO
SELECT orderid, empid
FROM [MyOrders]
WHERE [orderid] = '11077';
GO
SET STATISTICS IO OFF;
GO
```

Exexute queries with time statistic:
```sql
DBCC DROPCLEANBUFFERS;
DBCC FREEPROCCACHE;
SET STATISTICS TIME ON;
GO
USE lessons;
GO
SELECT orderid, empid
FROM [MyOrders]
WHERE [shipaddress] = '7890 Milton Dr.';
GO
SET STATISTICS TIME OFF;
GO

DBCC DROPCLEANBUFFERS;
DBCC FREEPROCCACHE;
SET STATISTICS TIME ON;
GO
USE lessons;
GO
SELECT orderid, empid
FROM [MyOrders]
WHERE [orderid] = '11077';
GO
SET STATISTICS TIME OFF;
GO
```

Add index to shippadress:

```sql
CREATE CLUSTERED INDEX IX_MyOrders ON [MyOrders]([orderid]);
GO
CREATE INDEX IX_MyOrders ON [MyOrders]([shipaddress]);
GO
```

Execute query with statistics again and compare.

You can see that one of the way to speed up query is just to add index :)

Try to execute sql:

```sql
USE lessons;
GO
DBCC DROPCLEANBUFFERS;
DBCC FREEPROCCACHE;
SET STATISTICS PROFILE ON;
SELECT orderid, empid, custid, shipaddress
FROM MyOrders
WHERE shipaddress = '7890 Milton Dr.';
GO
SET STATISTICS PROFILE OFF;
GO
```

Try to execute other sql:

```sql
USE lessons;
GO
DBCC DROPCLEANBUFFERS;
DBCC FREEPROCCACHE;
SET SHOWPLAN_TEXT ON;
GO
SELECT orderid, empid, custid, shipaddress
FROM MyOrders
WHERE shipaddress = '7890 Milton Dr.';
GO
SET SHOWPLAN_TEXT OFF;
GO
```
