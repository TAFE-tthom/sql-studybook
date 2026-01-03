# Structure of SQL Queries

SQL is a programming language designed for relational databases.

Unlike, a procedural or object-oriented programming language, it doesn't precisely outline how the data is retrieved. It leaves those details to the database engine and query optimiser.

SQL queries are generally referred as 'statements'.
This term is common in SQL and other programming languages.

## SQL Pattern

As a rough idea, we will prepare ourselves to understand SQL using the following format. It helps but we can see this model break when we create tables.

```
COMMAND_KEYWORD ([Identifiers/Expression])
([RELATED_KEYWORD (Identifiers/Expression)])
```

The above snippet probably doesn't mean much but it gives us a model of how sql statements are structured.

Lets take a look at a `SELECT` query.

```sql
SELECT firstname, lastname 
FROM people
WHERE lastname = 'Smith'
```

We can observe that the `SELECT`, `FROM` and
`WHERE` parts of the query are **keywords**.

The `firstname`, `lastname`, `people` components are identifiers.

The `lastname = 'Smith'` is an expression, in this case, narrowed down to be a predicate.

### Does our model hold?

How does this hold up to our model before?

```
COMMAND_KEYWORD     Identifiers

SELECT             firstname, lastname
```

The above, we can see how the identifiers were after the command keyword.

Since we are after the select statement, we need to use a keyword that is related to the `SELECT` command. In this case, `FROM` is related or expected to be used with `SELECT`.

```
RELATED_KEYWORD      Identifiers

FROM                 people
```

What makes this interesting is that the `FROM` keyword is valid when used with `SELECT` but might not be with others and it must be used after `SELECT` has been outlined. 

To note, a `SELECT` statement could be used without the `FROM` keyword but it might be a bit boring. However, we wanted to outline that it is optional.

Now we see a slight variation

```
RELATED_KEYWORD      Expression

WHERE                lastname = 'Smith'
```

We can see how the expression fits in here with
the related keyword and it is an expectation when
the `WHERE` keyword is used.

