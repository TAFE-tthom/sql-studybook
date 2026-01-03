# Modelling and Entity Relationship Diagrams

As part of database design, we need to identify the larger collections of data. In effect we need to identify what our tables are going to be.

Inside, we need to outline:

* What columns we will need to record
* What tables they connect to (primary keys/foreign keys)
* Particular data types assigned to columns
* Any additional constraints or formats


## ERD Types

There are different parts of the development of an ERD.

* Conceptual Diagram

Initial sketch of a database, usually table names, some columns but very much a visualisation of how the entities relate.

* Logical Diagram

Logical diagram where we move from the conceptual version and start adding specifics, clear connectivity and cardinality properties between tables. PK/FK column information and what will look like a base to start developing from

* Physical Diagram

What the database will look like, from the logical diagram but it will have clearer specifics around datatypes and database specifics like constraints and unique indexes.


### Notations

There are typically two preferred methods to represent/draw an ERD.

* Crow's foot notation
* Chen's Notation

## Selecting Datatypes

> Age and employee numbers are simple whole numbers.

A description like this gives an idea on how the data is to be represented but not specifically the most appropriate type.

Given that age changes over time and arithmetic operations are appropriate to this field, it is appropriate to declare it an INT.

*But what about employee numbers?*

These are less obvious, these could be integer or they could be represented a string.

*What questions could you ask to clarify and help select an appropriate data type?*

* Are employee numbers prefixed?
* Do they change frequently and how do they change?


## Relations

> Employees have tasks associated to them which are issued by other managers (which are also employees).

This is an interesting problem, but we can identify two concepts:

* Employees
* Tasks

We can represent these tables as blocks within the diagram and connect them logically but also in the physical version, outline the joining table.

*However, how do we relate these two tables?*

We can have employees by itself but tasks have two columns which would refer to employees.

* Issuer
* Assigned

And a requirement where the Issuer's range is also relevant to who they manage.

While the previous intuition around referring to the employee table for both columns, it doesn't meet the requirement outlined.

So, how could we solve this?

*Could we create a Managers table?*

Which refers to the employee table but have their own manager ID.

*Is that enough though?*

No, because we want to know specifically if that employee is a higher rank!

So what could we do?

* How about we introduce a managed list or what group the manager is associated with?
