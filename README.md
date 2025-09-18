#  Library Management System using PostgreSQL
## The system will manage a collection of books, authors, and patrons. Users are be able to add, view, update, and delete records in the database.

- creating databse
```
create database libraryDB;
```

- Creating tables using the create keyword
```
-- creating database
create database libraryDB;

-- creating authors table
create table authors(authorId serial primary key, a_name varchar(255),nationality varchar(255),birth_year int not null,death_year int);

-- creating the books table
create table books( bookId serial primary key, title varchar(255) not null,authorId int references authors(authorId),genres text[] default'{}',published_year int, availability boolean default true  );

-- creating patrons tables
create table patrons(patronId serial primary key,p_name varchar(255),email varchar(255) unique,borrowed_books int[] default '{}');
```

