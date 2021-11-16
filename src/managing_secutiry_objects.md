# Managing Security Objects

SQL Server logins, users, and roles have their own corresponding CREATE and DROP statements. The syntax for creating a new login is slightly different depending on whether the new login is a Windows login or a SQL Server login.

We will look into only login related to SQL Server login

```sql
USE Master
GO
CREATE LOGIN viktor WITH Password = 'P@ssword1' USE lessons
GO
CREATE USER viktor FOR Login viktor
```

Drop user

```sql
USE lessons
GO
DROP USER viktor
GO USE Master
GO
DROP LOGIN viktor
```