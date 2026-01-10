# Database Users, Roles and Memberships

## What is DCL?

Data Control Language, this component is focused on the following database constructs such as:

* User
* Roles
* Permissions
* Passwords

SQL vendors outline their method of implementing security as well as the other criteria of managing it or integrating it with other security/permission models.

## Grant, Revoke, Deny

We have the following, keywords that allow us to apply different rules on users for a particular object or role.

* `GRANT`, gives access/privileges to a user for a database object.

* `REVOKE`, remove access/privileges to a user for a database object.

* `DENY`, Denies permission to a database object.


### Permissions

The permissions that can be enacted on can be operated on specific tables and databases. It will also impact what operations they can do.

This includes DDL and DML operations.

Commonly, you will use `GRANT`, `REVOKE` and `DENY` operation specifying their permissions on `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE`, `ALTER` and `DROP`.

#### Grant

```sql
GRANT ALL ON thedb.* TO 'jeff'@'localhost';
```

This will grant all permissions on all database object that is part of `thedb` object. These are normally different schemas that are associated with it.

Specifically we can enforce a rule on `INSERT` where a user may get permissions to perform `INSERT` on the table. The snippet below will outline on all the tables associated with the database `world`.

```sql
GRANT SELECT ON world.* TO 'role3';
```

We can specify permissions on select tables.

```sql
GRANT SELECT ON thedb.Books TO 'jeff';
```

We can be specific and specify multiple parts on the role or user.

```sql
GRANT INSERT, UPDATE, SELECT ON thedb.Authors TO 'role3';
```

#### Revoke

```sql
REVOKE ALL ON thedb.* TO 'jeff'@'localhost';
```

The above statement will revoke all the permissions that 'jeff' has associated with them. This will result in the user not being able to utilise any object part of `thedb` on the server.


*What about `DENY`?*

`DENY` and `REVOKE` can seem like they are fulfilling similar roles here. For the most part, they can be used similarly, however `REVOKE` is to ensure that any permissions given have been removed.

`DENY` however, is checked before anything else, if a `DENY` exists on an object for a particular role or user, even if the permission was granted, the operation would not succeed.
