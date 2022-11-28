SQL Course
----------

# Terminology and basic SQL

* Relational databases: Postgres, MySQL, Oracle, MS SQL
* Clients: DBeaver, JetBrains products
* Table/relation, record/row/tuple, schema, database
* Connection string
* Select, projection
* `count()`
* Conditions: =, >, <, !=, <>, in, like, ~, ~~, is null
* Sorting
* Table and column aliases
* Conventions. "Name" vs Name
* Formatting

Homework:

1. Connect to the database
2. Look through the tables and their columns - find some corresponding entities and their attributes on UI
3. Try changing something on the UI and see the database state change accordingly
4. Select chromatograms of injections with name that ends with 01
5. Select peaks of some injection, sort peaks by area
6. Select Injections of a Batch, order them by Acquisition Time. Now try by Name desc.
7. Find chromatograms in some injection with no association with substances (not EICs)

# Joins

* Unique columns (Keys), Primary Key, Secondary Key
* Foreign Key
* Select from multiple tables without joins
* Joining 2 tables: get chromatogram with peaks
* Joining 3 tables: get injection with chromatograms and their peaks
* One-to-One, One-to-Many, Many-to-Many
* Outer joins (Left, Right), Inner join. The default is different for different vendors.
* Additional joining conditions
* `using` keyword

Homework:

1. Find all injections that have substances in them
2. Get all batches with all the peaks inside them
3. Find batches and their peaks, but this time we're interested only in peaks on Total chromatograms (see `chromatograms.total` column)

# Subselect, case

# Grouping, aggregating functions

* Unique substances within peaks
* Number of peaks in injection
* Injections with n of peaks > 0
* Distinct keyword
* Group by multiple fields: injections w/ 2 peaks and 2 substances
* Get injection w/ max number of peaks, join them with peaks
* Aggregation functions: count(), max(), min(), avg(), sum(), percentile()
* listagg

# Data types, functions, casting

* Strings: upper(), lower(), replace(), concat()
* Numbers
* Dates: truncate, get day, month, etc
* Interval

# Selecting from expressions

* CTE
* Selecting from functions: `now()`, `random()`, `generate_series()`
* Cross join

# Window functions

# Indexes