# DQL and DML

Within theis chapter we will be covering the basics to querying and manipulating data within existing schemas. DQL (Data Query Language) and DML (Data Manipulation Language) components are focused around the following areas within SQL.

1. Select - Retrieving Records
2. Insert - Creating Records
3. Update - Updating Records
4. Delete - Removing Records

There is an assumptions for most of this chapter that we will be using the `Sakila` database. You can access this schema and its data within the **resources** section of this chapter.

## Loading a predefined schema and data

Outside of developing an application from scratch, it is rare that you will be designing and implementing a database from scratch. You will typically be maintaining and interacting with an existing database.

You have access to the following databases:

* Northwind
* Sakila

A predefined schema and set of data can come show up in a few different ways.

* Database File - Typically loaded by the database server process during start up.

* SQL Schema File - Text file that contains database creation and tables.

* SQL Data - Text file that typically contains a set of insert statements that prefill the data.

There are pros and cons to loading a database vs the sql text files.

## Binary Files and Text Files

The database file runs the risk of having some optimisations that may be only suitable for the current environment and run-time of the server. It is what is used by a database in its current environment.

The text representation are resembling what someone would write as a query or as part of an operation from an application that connects to a database.

