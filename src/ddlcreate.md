# DDL and Creating Databases

There are two tasks we will be focusing on. We will be creating a database and a schema for that particular database.

## Creating a database

First action we will do is create a database on our newly created MariaDB server.

```
CREATE <RELATED_KEYWORD> <IDENTIFIER> 
```

Lets create our library database.

```sql
CREATE DATABASE LibraryDB;
```

We can observe the structure of the statement and the creation of our database on our server.


We now want to `use` our database.

```sql
use LibraryDB;
```

We specify this so, we know what database on the server we are using. Since a server can have multiple databases, we need to specify which one we want to use.

> **Author's Note:** Most but not all SQL implementations operate like this. Something like **SQLite** which is a file-backed SQL implementations doesn't have a clear need for the `use` keyword.

**Time to Check**

Before moving on to the next section, you will need to ensure you have the following completed.

* Have you connected to your database?
* Have you created a database called `LibraryDB`
* Have you specified the database with the `use` keyword?


## Creating Tables

Now we can get on creating tables which is where our database comes alive.

```sql
CREATE TABLE Book(
    Id INT,
    ISBN CHAR(13) NOT NULL,
    Title VARCHAR(100) NOT NULL,
    Description VARCHAR(500) NULL,
    UnitPrice INT NOT NULL
)
```

The above sql query creates a table called `Book`, with five columns (Id, ISBN, Title, Description, UnitPrice).

### Columns and Datatypes

Tables have columns, each column will have an identifier and a datatype. Columns can be extended to do a a lot more as we will see later.

Items inserted into a table are typically referred as **tuples** or **entries**.

As what you noticed here is that each column has a description as part of its identifier.

```sql
    Id INT,
    ISBN CHAR(13) NOT NULL,
    Title VARCHAR(100) NOT NULL,
    Description VARCHAR(500) NULL,
    UnitPrice INT NOT NULL
```

Let's decompose the above datatypes.

* Id, is an INT datatype, it means that accepts integer numbers (1, 2, 3... 100, -1, -2)

* ISBN is a CHAR and is also specified as NOT NULL, ISBN limit is that it will only accepted up to **13** characters. It also means it is exactly 13 characters. Any less and it pads it with '\0' characters. 

* Title is a VARCHAR(100), it will accept up to 100 characters, but it will not pad.

* Description is similar to Title but it can be
excluded, as it is **NULLABLE**.

* UnitPrice is an INT and is required.


#### Datatypes

There are a lot of different datatypes and these can also categorised into:

* Boolean (True or False) 
* Numeric
    * INT
    * DECIMAL
    * FLOAT 
* Text/String
    * CHAR
    * VARCHAR
    * BLOB

* Date and Time
    * DATE
    * DATETIME
    * TIMESTAMP

While other SQL servers may have more comprehensive datatypes such as `MONEY`, these are usually aliases and not part of the SQL standard.

##### Text Datatypes

As with most programming languages we have a way we categorise data. SQL is no different in this case, depending on what data you want to record, you want to select and use most suitable datatype to represent this.

Each datatype has suitable operators associated with it. We will look at the TEXT datatypes now.

For text data, this is usually expressed between single quotes like so:

```sql
'This is text'
```

And the following data types are appropriate:

* `CHAR(size)` - Fixed number of characters

* `VARCHAR(size)` - Up to the number of characters.

* `TEXT` - Arbitrary size


##### Numeric Datatypes

We now look at datatypes that represent numbers.

There are two common representations of numbers. `INTEGER` and `REAL` (`REAL` is usually referred to as `FLOAT` or `DOUBLE`).

`INTEGER` or `INT`, represent the integer set of numbers, these are number which are not fractions such as `-1`, `1` and `10`.

`REAL` or `FLOAT`, are floating point numbers, these have a precision component and are intended to represent the real number set.

`BOOLEAN`, which is a representation of an integer, represents two values. `true` and `false`.

This representation is useful for making decisions with code.

The boolean datatype is a little bit special as we usually rely on this datatype as part of logical expressions. We will be exploring this later.


##### Datetime Datatypes

A common and often overlooked format is the date time datatype. This is because this datatype is usually an abstraction on string and numbers however does intersect both datatypes.

`DATE` - Only represents the date itself, this will result in the required data to represent not needing to incorporate a time component. It can make it a little imprecise but can be suitable for most needs.

`DATETIME` - Will incorporate a time component within the datatype, this will need to include the year, month, day along with hour, minute and second. 

`TIMESTAMP` - A timestamp is normally a numeric representation in seconds (or milliseconds) of the datetime. It is relative to a certain point in time (commonly Unix Epoch) and can be converted to DATETIME and DATE. However since it is relative to a particular point and is a numeric representation, its usecases are very apparent for transactions and logging but less so for historical data.


##### Nullables

* When defining columns within SQL, you can also specify if the
    column is `NULL` or `NOT NULL`.

This qualifier, indicates if the the data is needed when inserting data into the table.

As a general rule, you should try to avoid nulls although they will be part of your life/programming careers, the abscence of things and therefore making assumptions that it exists leads to issues not just in SQL but with programming languages in general.


### Tuples

Tuples capture the data in a table row. They are usually referred to as tuples that since our queries are not just operating on a single table but potentially multiple tables, they allow us to articulate clearly the grouping of data.

```sql
SELECT Id, ISBN, Title, UnitPrice FROM Book;
```

The above will return one or many tuples that include Id, ISBN, Title and UnitPrice.

### Review

Quickly review the above sections and double check your understanding against these questions.

* What is a table?
* What is a column?
* What is a datatype?
* What kind of datatypes do we have?

