# SQL

- [SQL](#sql)
  - [Relational databases](#relational-databases)

## Relational databases

- A way to describe relationships between data entities
- Relational model built on top of the mathematical concept of Tuple relational calculus
- Implementation via Tables, with a table name, columns and rows
- Database normalization done so that we can query the database to get relevant results.
  - Say we intent to store user's contact information, name and emailId.
  - Poor way to design is to have a single table and add a column for name and emailId. But what if a user has more than one emailId? What if I want to ask questions like how many userIds do users have on average?
  - Better way would be to we create two tables, `Contact` table and a `Email` table connected via Keys.
  - This lets us ask questions like what are Person A's email addresses
