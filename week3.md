# Weekly Objectives:
- Design a database schema with at least two tables from a specification, including a one-to-many relationship between two tables, and create the schema in a database using SQL.
- Use SQL to query a database to read data from one table or resulting of a join, create new records, update and delete.
- Integrate a relational database to a program by test-driving classes which implement CRUD methods to send SQL queries to a database.

# Day 1 Notes

## Into to PostgreSQL

PostgreSQL is the rational database (based on SQL).
Allows to:
- Create data
- Update data
- Delete data
- Read data
*Applications whch can talk to a database are called **CRUD** *

Usually one database per project.
Can contain multiple tables.

## Querying data

```
SELECT [columns to select] FROM [table name];
```
- used to retrieve records from a table
- the otput is called a **result set**

We can also filter data:
```
SELECT [columns to select] FROM [table name] WHERE [conditions];

-- e.g. 
SELECT release_year FROM albums WHERE title = 'Bossanova';
```

## Keys

**Primary key** - First column, every table has one, unique
**Foreign key** - Connects data points to the other table

## Updating and deleting data

```
UPDATE [table name] SET [column_name] = [new_value];

UPDATE [table name] SET [column_name] = [new_value], [other_column_name] = [other_new_value];

-- e.g.
UPDATE albums SET release_year = 1972 WHERE id = 3;

DELETE FROM [table name] WHERE [conditions];

-- Or, delete all records (never do this!)
DELETE FROM [table name];

-- e.g.
DELETE FROM albums WHERE id = 12;
```
## Creating new data

```
INSERT INTO [table name]
  ( [list of columns] )
  VALUES( [list of values] );
  
-- e.g. 
INSERT INTO albums
  (title, release_year)
  VALUES('Mezzanine', 1998);
  
INSERT INTO artists
  (name, genre)
  VALUES('Radiohead', 'Alternative');

INSERT INTO albums
  (title, release_year, artist_id)
  VALUES('OK Computer', 1997, 6);
```
## Connecting Ruby and PostgreSQL

- Model class
  - Hold a recoder's data
  - e.g. class **Student** for table `students`, w/ _attributes for each column_

- Repository class
  - Implements methods to run SQL queries
  - e.g. StudentRepository

### Mapping of classes

```
project/
   app.rb
   lib/
      student.rb
      student_repository.rb
   spec/
      student_repository_spec.rb
```

***Object-relational mapping*** - converting records from a database into objects we use in our program


