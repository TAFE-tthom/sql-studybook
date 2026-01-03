# Exercises

For each chapter you will have a set of exercises to complete.

## Tasks

### 1. Create Table

You have been tasked with creating a table that will hold data about books. The Book table will need to hold the following information:

    isbn_11, CHAR(12) - ISBN number that will be used as a primary key.
    title, VARCHAR(56) - Title of the book
    description, VARCHAR(200) - A simple description of the book.

Make sure it meets the above specifications and that you use CREATE TABLE, to ensure that the table is created and ready for data to be inserted.


### 2. Authors and Books

Using your table you have created from the last exercise, you will need to introduce a new table and also introduce a new column in Book.

You will need to create a table called Author, which will contain the following columns.

    author_id, INT - An integer identifier for the author, this is also the primary key.
    first_name, VARCHAR(50) - First name of the author.
    last_name, VARCHAR(50) - Last name of the author.

Please note: Order of statements does matter! If you use a foreign key, the table it is referring to must already exist before executing it.

With the Book table, most of the columns will remain the same however author_id will need to be introduced into your create table statement.

    isbn_11, CHAR(12) - ISBN number that will be used as a primary key.
    title, VARCHAR(56) - Title of the book
    description, VARCHAR(200) - A simple description of the book.
    author_id, INT - Foreign key that refers to Author table.

Make sure it meets the above specifications and that you use CREATE TABLE, to ensure that the table is created and ready for data to be inserted.


### 3. AutoIncrement

You will need to create a table called Ticket, what is special about this table is that the primary key will be automatically generated upon insertion.

The table will have the following columns.

    ticket_id, INT - When a new ticket is added to the table, the id will be generated (incremented). Make sure you use AUTOINCREMENT and set this as the primary key.

    ticket_origin, VARCHAR(50) - Store a username based on who created the ticket.

    ticket_description, VARCHAR(500) - Description of the ticket.

    resolved, BOOLEAN - Outlines if the ticket has been resolved or not.

When inserting data into this table, it shouldn't be required to specify the ticket_id column in the INSERT statement.


### 4. Dropping Tables

ou have been given the task of removing tables that someone broke during development.

The following tables are unnecessary and will need to be removed.

    InvoiceLogs
    PaymentProcessors

The remaining tables should be:

    Product
    LineItem
    Sale

Make sure you use the correct syntax in this exercise.


### 5. Alter Tables

Oops! Someone forgot the discount column in the Product table.

Could you please ALTER the table and add the column discount with the datatype DECIMAL.

The above exercise follows on the from previous exercise (4).
