# Domain Rules and Checks

When constructing a database there are rules which exist in the real work that we need to encode within it. While it is very feasible to simple encode these rules within the application that is normally paired with the database. The same rules can also be applied here as well.

While it can appear limiting as, when you create a constraint, that same constraint may need to be undone later on. However these are normally rules which are established and for the ensuring data integrity.

## Default Values

A simple idea is the idea of a default value to be applied onto a column. These are usually sensible defaults like the duration of a subscription when newly inserted data has been given.

```sql
CREATE TABLE Customer (
  customer_id INT NOT NULL,
  name VARCHAR(512) NOT NULL,
  age INT NOT NULL,
  last_activity TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

The above table outlines a column called `last_activity` in which the timestamp is the `CURRENT_TIMESTAMP`. This is a good default value as this likely indicates that the user has recently signed up taking the current timestamp as a default value is reasonable.


## Check Constraints

A check constraint allows us to provide a rule onto the data itself. We can enforce constraints
on the data existing and inserted to abide by this rule.

A example could be to ensure that any person buying tickets for a concert is 18 or above.

```sql
CREATE TABLE Customer (
  customer_id INT NOT NULL,
  name VARCHAR(512) NOT NULL,
  age INT NOT NULL
  CHECK (age >= 18)
);
```

So, consider what kind of constraints we would want to enforce on a table?

What kind of examples can you come up with?
