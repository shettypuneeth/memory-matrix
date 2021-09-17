# SQL

- [SQL](#sql)
  - [Relational databases](#relational-databases)
  - [Basic syntax](#basic-syntax)
  - [Basic commands](#basic-commands)

> Notes taken from [Introduction to SQL](https://app.pluralsight.com/library/courses/introduction-to-sql/table-of-contents)

## Relational databases

---

- A way to describe relationships between data entities
- Relational model built on top of the mathematical concept of Tuple relational calculus
- Implementation via Tables, with a table name, columns and rows
- Database normalization done so that we can query the database to get relevant results.
  - Say we intent to store user's contact information, name and emailId.
  - Poor way to design is to have a single table and add a column for name and emailId. But what if a user has more than one emailId? What if I want to ask questions like how many userIds do users have on average?
  - Better way would be to we create two tables, `Contact` table and a `Email` table connected via Keys.
  - This lets us ask questions like what are Person A's email addresses

## Basic syntax

---

A SQL statement is an expression that tells a database what to do.

Sample expression

| keyword | identifier | keyword | identifier |
| ------- | ---------- | ------- | ---------- |
| SELECT  | first_name | FROM    | person     |

`SELECT first_name` is a select clause, that tells the DB what do we want.
`FROM person` is a from clause that tell the DB where do we want it from.

## Basic commands

---

1. SELECT
   - Retrieves one or more rows from one or more tables
2. INSERT
   - Insert one or more rows into a table. Works only with a single table.
   - `INSERT INTO contacts (first_name, last_name) VALUES ('John', 'Carter');`
   - Need not specify an id column as that's auto-generated via database design.
3. UPDATE
   - Modifies one or more rows
   - `UPDATE contacts SET last_name='Smarter' WHERE id = 1;`
4. DELETE
   - `DELETE FROM contacts WHERE id = 1;`

> Table names to be singular by convention.
> <br/> Goes by the logic that Table name should be about each row is about.
> <br/> E.g if you're storing contacts information, the table would be `Contact` as each row is a contact.

Understanding the fundamentals of SQL will allow us to ask the right questions about the data stored in the DB and draw conclusions from the results.
