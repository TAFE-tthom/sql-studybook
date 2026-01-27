# Review

Revealing that we have been transactions provides us with insight into how the data is able to batch reads and writes together and ensure data integrity. This concept is occasionally tricky to apply without first knowing what the performance profile is like.

* What you should know and understand
  * What a transaction is and how it relates to the queries you have written
  * Exceptions that can occur during a transaction
  * What a rollback, commit and savepoint feature sets are doing
  * What the transactions states are
  * How stored procedures and functions are used and their relationship

* What you should be able to apply
  * Implement a transaction that makes multiple modifications in multiple tables
  * Performance implication of a transaction and why batching is appropriate
  * Constructing a stored procedure and a function
  * Apply using your own stored procedure and functions in appropriate contexts
