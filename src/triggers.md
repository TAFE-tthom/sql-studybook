# Triggers and Events

Triggers allow queries to be executed on an event that occurs on a table.

Typically for INSERT, UPDATE and DELETE, we are able to trigger a query that occurs before the mutation occurs or after.

Scenarios:

* Maintaining a column that shows the last time an entry was updated
* Keeping a log of transactions
* Keeping a log or state of batch operations (before and after triggers)


```sql
CREATE TRIGGER ins_transaction BEFORE INSERT ON account
       FOR EACH ROW PRECEDES ins_sum
       SET
       @deposits = @deposits + IF(NEW.amount>0,NEW.amount,0),
       @withdrawals = @withdrawals + IF(NEW.amount<0,-NEW.amount,0)
```

The above is a trigger called `ins_transaction` which occurs before an insertion of a record happens on the `account` table.

This will update the current deposits and withdrawals totas for all each row in `ins_sum`.

Similar to stored procedures the construction of a trigger will need to refer to a different set of delimiters instead of the default `;`.

* `NEW` is referring to the newly new entry.
* `OLD` is referring the existing/old entry within the dataset.

## Pre and Post Events

Triggers have two properties associated with them. These relate to when they are triggered on a particular table.

The different events occur either `BEFORE` or `AFTER` the event itself which could be an `INSERT`, `SELECT`, `UPDATE` and `DELETE`. The other property is for determining how the trigger will work on the dataset itself.

It isn't as simple as operating on the newly inserted data as the trigger could be responsible recalculating/deriving data but could be impacted by another trigger or event. This will either be `PRECEDES`, `FOLLOWS`, or normally left blank. This can seem confusing but it is in relation to when there are more than one trigger that can be applied onto a table or related to it.

* Without specifying, it is assumed that it is unaffected by other triggers.
* `PRECEDES` - This will need to know if the trigger is going to occurr before another.
* `FOLLOWS` - This will need to know if the trigger should be applied after another.


