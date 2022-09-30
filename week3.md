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

## Relationship in Relational Databases

One-to-many
- most common
- one record in a table associated with many records in another table
- e.g. One blog post can be associated with many records of comments
- designed by creating the foreign key

# Day 4 Notes

```SQL
SELECT albums.id AS album_id, -- can specify the name of the column to avoid ambiguity
       artists.id AS artist_id,
       albums.title,
       artists.name
  FROM artists 
    JOIN albums -- will be first to specify on the next line
    ON albums.artist_id = artists.id 
  WHERE artists.name = 'ABBA'; -- can also filter the selection
```

# Day 5 Notes

## Many-to-many relationships

- _When a record from the first table can have many records in the other table, and the other way is also true._
- e.g. posts and tags
- made with a joint table consisting of two foreign keys (e.g. posts.id and tags.id)

```SQL
-- Select all the tags associated with a given post.
-- Note how we're using two different joins to "link"
-- all the three tables together:
--    * first, by matching only records in the join table for the given post
--    * second, by matching only tags for these records in the join table
SELECT tags.id, tags.name
  FROM tags 
    JOIN posts_tags ON posts_tags.tag_id = tags.id
    JOIN posts ON posts_tags.post_id = posts.id
    WHERE posts.id = 2;
    
    
```

**Linking two records**
- need to insert a **new record** into a **joint table** using **two primary keys** of records which needed to be linked together
