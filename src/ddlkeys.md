# Keys and Constraints

Keys and constraints are a major components of **Relational Databases**.
These lean into the relational part where we can link tables together by specifying what columns are keys.

## Primary Keys

Lets recreate our `Book` table, however we will add a `PRIMARY KEY` to our table.

```sql
CREATE TABLE Book(
    Id INT NOT NULL,
    ISBN CHAR(13) NOT NULL,
    Title VARCHAR(100) NOT NULL,
    Description VARCHAR(500) NULL,
    UnitPrice INT NOT NULL,
    PRIMARY KEY (Id)
);
```

We can observe we have specified that the `Id` is the primary key, which
has the following rules:

* This value has to be unique, there can only be a 1 book with the Id, 200 as an example, you cannot have duplicates.
* It must not be null, a value must always exist.

Alternatively, we can also be clear with the kind of constriant and naming of the primary key.

```sql
CREATE TABLE Book(
    Id INT NOT NULL,
    --- snipped rest ---
    CONSTRAINT PK_Book PRIMARY KEY (Id)
);
```

The above variant names the primary key but it is useful to know this method as it allows us **compose** keys together (composite primary keys). 


### Primary Keys and AutoIncrement

Lets create a couple of new tables to demonstrate composite keys and see other features of primary keys.

```sql
CREATE TABLE Customer
(
	Id INT AUTO_INCREMENT	PRIMARY KEY,
	FirstName VARCHAR(100) NOT NULL,
	LastName VARCHAR(100) NOT NULL
);
```

**What is interesting here?**

We can observe the `Id` is a primary key but also has an `AUTO_INCREMENT` qualifier, this means the value of `Id` on newly inserted rows will increment by 1. This means it can be absent on an `INSERT` statement.

Alright lets now create a `Review` table, this table will look like the following:

```sql
CREATE TABLE Review
(
	CustomerId INT,
	BookId INT,
	CONSTRAINT PK_Review PRIMARY KEY (CustomerId, BookId)
);
```

The above `CONSTRAINT` statement shows that the primary key uses two columns, this is known as a composite key.



## Foreign Keys

This leads us to `FOREIGN KEY`s, these keys are used to reference other tables. We can do this on creation of a table or by altering it.

```sql
ALTER TABLE Review
ADD COLUMN
Comment VARCHAR(500) NULL,
StarRating INT not null;

ALTER TABLE Review
ADD CONSTRAINT FK_Review_Customer FOREIGN KEY (CustomerId)
REFERENCES Customer (Id),

ALTER TABLE Review
ADD CONSTRAINT FK_Review_Book FOREIGN KEY (BookId)
REFERENCES Book (Id);

```

We have added 2 new columns, `Comment` and `StarRating` because we need something interesting with the reviews. However we have added tow new constraints.


```sql
ALTER TABLE Review
ADD
--- Snipped the rest ---
CONSTRAINT FK_Review_Customer FOREIGN KEY (CustomerId)
REFERENCES Customer (Id),
CONSTRAINT FK_Review_Book FOREIGN KEY (BookId)
REFERENCES Book (Id);

```

The two keys here are changing the columns `CustomerId` and `BookId` to reference the tables `Customer` and `Book` and their primary keys.

Which means that a value for the columns `BookId` and `CustomerId` in review must also exist in `Customer` and `Book`. If it does not, it is rejected.

Foreign keys are fairly straight forward, they are a constraint that
allows us to refer to another table's entry.

Here are some good uses for primary keys and foreign keys.

* Students and Subjects, we want to ensure have a clear idea if a student is enrolled in a subject and what students are part of a subject. A table that has StudentID and SubjectID where StudentID will reference the Students table and SubjectID references the Subjects table.

* Orders and Products, we may want to know what products are in an order.



## Dropping Tables

Now at the end here, we may want to discard or redo tables.

We are able to `DROP` tables by using the `DROP` keyword.

```sql
DROP TABLE Reviews;
DROP TABLE Book;
DROP TABLE Customers;
```

The above statement will remove each table, however, in the event that we drop a table that is being used by another, we mught trigger a violation. Make sure you attempt to drop them in order.

