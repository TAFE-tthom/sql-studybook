# Altering Tables

Once a table has been created, we could find ourselves feeling
trapped and needing to change it or remove it entirely.

Through out this chapter we will be using the `LibraryDB` database and demosntrate modifications by modifying the `Book` table.


## Manipulating Tables

```sql
ALTER TABLE Book
ADD COLUMN
Category VARCHAR(100) NOT NULL;
```

The above statement will allow us to alter the table and `ADD` a
new column to the table.

We are also able to modify specific columns.


### Modifying Columns

In the table above, we are able to modify the column of the `Book` table.

```sql
ALTER TABLE Book
MODIFY COLUMN
UnitPrice FLOAT NOT NULL;
```

The above will change the type of `UnitPrice` but we have to be
careful with what data that may exist inside it. It may not be something easily convertible.

We can also remove columns by using `DROP` keyword when altering a table.

```sql
ALTER TABLE Book
DROP COLUMN
Category
```

This will remove the `Category` column from the `Book` table.

**Always check your changes, simply just run a select query on the table and observe the changes**


We will be exploring more altering of tables in the next section by adding and modifying tables to incorporate keys.

