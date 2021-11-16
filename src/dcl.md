# DCL

Three SQL statements are used to control permission to all database objects and securable user resources (that is, users and roles). Each statement accepts the permission type (select, insert, update, delete, execute, and so on), the object name, and the user or role to which the setting applies.

* GRANT:

```sql
GRANT INSERT ON Production.Product TO viktor
```

* DENY:
  
```sql
DENY INSERT ON Production.Product TO Paul
```
* REVOKE

```sql
REVOKE INSERT ON production.Product TO Paul
```


