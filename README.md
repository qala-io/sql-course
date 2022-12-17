SQL Course
----------

# Step 1: Terminology and basic SQL

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

### Homework:

1. Connect to the database
2. Look through the tables and their columns - find some corresponding entities and their attributes on UI
3. Try changing something on the UI and see the database state change accordingly
4. Select injections with name that ends with 01
5. Select peaks of some injection, sort peaks by area
6. Select Injections of some Batch (open a batch, take its ID from address bar), order them by Acquisition Time. Now try by Name desc.
7. Find chromatograms in some injection with no association with substances (`substance` column is null)

# Step 2: Joins

* Select from multiple tables without joins
* Unique columns (Keys), Primary Key, Secondary Key
* Foreign Key
* Joining 2 tables: get chromatogram with peaks
* Joining 3 tables: get injection with chromatograms and their peaks
* One-to-One, One-to-Many, Many-to-Many
* Outer joins (Left, Right), Inner join. The default is different for different vendors.
* Additional joining conditions
* `using` keyword

### Homework:

1. Select all the injections that aren't added to any batches, ordered by import time. We should get the same records as [this page](https://sqlcourse.peaksel.elsci.io/injections) shows.
2. Get all the peaks in all batches sorted by Area. Note, that peaks reference injections, and injections reference batches. So there will be 3 tables involved.
3. Find batches and their peaks, but this time we're interested only in peaks on Total chromatograms (see `chromatograms.total` column)
4. Count the number of rows in the last query. And compare it to the number of rows we got before that.

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

### Homework: 

1. For each day of current and previous years, get the number of injections uploaded. Days without injections should have 0.
2. There are 5 dice: two are 4-sided (numbers 1 through 4) and the other 3 are 6-sided (numbers 1 through 6). What's the probability the sum is going to be 15? To figure it out you need to generate all possible combinations of these 5 dice, then count the number of combinations that sum up to 15 and number of all possible combinations. Then divide one by the other. 
3. We will consider a famous Tuesday Boy problem in Probability Theory. Our goal would be to generate a set of rows and then calculate probabilities (frequencies).

<details>
<summary> <b>Problem1 - probability of a boy given families with at least one boy</b></summary>

There's a set of families with 2 children. We're interested in families where at least one of the kids is a boy. When selecting a random family out of this set, what's the probability that there are 2 boys?

Feel free to calculate the probability, but then we'll need to check it with SQL:

1. Generate a set of rows that represent families. Columns: `child1_boy` (boolean), `child2_boy` (boolean). The each value could be either `true` or `false` with 50% chance.
2. Out of the set, filter out families that don't have boys
3. And finally count a) families with 2 boys b) number of all families. Then calculate the proportion of one to another

Is the result consistent with what you predicted?
</details>

<details>
<summary> <b>Problem2 - probability of a boy given families with at least one boy born on Tue</b></summary>

Now the condition is a little more complicated: our families have at least one boy born on Tue. When selecting a random family, what's the probability it's a boy?

1. Let's add 2 additional columns to our generated data set: `child1_weekday`, `child2_weekday`. Use either numbers or strings to denote days of weeks. Each day is equally probable.
2. From the generated set filter out only rows where there's at least one boy. And at least one of the boys has birthday on Tue.
3. Now calculate the proportion of families with 2 boys

Does the result surprise you? Can you explain why this is the case?

</details> 

# Window functions

# Indexes