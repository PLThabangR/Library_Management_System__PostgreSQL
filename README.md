#  Library Management System using PostgreSQL
## The system will manage a collection of books, authors, and patrons. Users are be able to add, view, update, and delete records in the database.

### To run this project ensure you have installed 
- PostgreSQL (latest stable version)
- pgAdmin (optional, GUI)
  
- create the database
```
create database libraryDB;
```
- In pgAdmin: Right-click → Query Tool → paste → Execute

- Then create tables using the create keyword copy and paste the below statements
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
- Inseting values into the table
- To insert values in your database copy and paste the below 
```
insert into authors(a_name,nationality,birth_year,death_year) values ('George Orwell', 'British', 1903, 1950),
('Harper Lee', 'American', 1926, 2016),( 'F. Scott Fitzgerald', 'American', 1896, 1940),
('Aldous Huxley', 'British', 1894, 1963),('J.D. Salinger', 'American', 1919, 2010),
('Herman Melville', 'American', 1819, 1891),('Jane Austen', 'British', 1775, 1817),
('Leo Tolstoy', 'Russian', 1828, 1910),( 'Fyodor Dostoevsky', 'Russian', 1821, 1881),
('J.R.R. Tolkien', 'British', 1892, 1973);

-- insert data to books table
 insert into books(title, authorId, genres, published_year, availability)values 
 ('1984', 1, ARRAY['Dystopian', 'Political Fiction'], 1949, TRUE),
 ('To Kill a Mockingbird', 2, ARRAY['Southern Gothic', 'Bildungsroman'], 1960, TRUE),
 ('The Great Gatsby', 3, ARRAY['Tragedy'], 1925, TRUE),
('Brave New World', 4, ARRAY['Dystopian', 'Science Fiction'], 1932, true),
('The Catcher in the Rye', 5, ARRAY['Realist Novel', 'Bildungsroman'], 1951, TRUE),
( 'Moby-Dick', 6, ARRAY['Adventure Fiction'], 1851, TRUE),
('Pride and Prejudice', 7, ARRAY['Romantic Novel'], 1813, TRUE),
('War and Peace', 8, ARRAY['Historical Novel'], 1869, TRUE),
('Crime and Punishment', 9, ARRAY['Philosophical Novel'], 1866,true),
( 'The Hobbit', 10, ARRAY['Fantasy'], 1937, TRUE);


 Insert data to patrons table
insert into patrons(p_name,email,borrowed_books)
values( 'Alice Johnson', 'alice@example.com', ARRAY[]::INT[]),
('Bob Smith', 'bob@example.com', ARRAY[1, 2]),
( 'Carol White', 'carol@example.com', ARRAY[]::INT[]),
('David Brown', 'david@example.com', ARRAY[3]),
('Eve Davis', 'eve@example.com', ARRAY[]::INT[]),
('Frank Moore', 'frank@example.com', ARRAY[4, 5]),
( 'Grace Miller', 'grace@example.com', ARRAY[]::INT[]),
( 'Hank Wilson', 'hank@example.com', ARRAY[6]),
('Ivy Taylor', 'ivy@example.com', ARRAY[]::INT[]),
( 'Jack Anderson', 'jack@example.com', ARRAY[7, 8]);

``` 


- Read oprations
```
select * from books;


-- Get book by title
select *  from books
where title ilike '1984'

-- Get all books by author using joins
select *  from books as a
join authors as b on a.authorId = b.authorId
where b.a_name = 'J.R.R. Tolkien';
 

-- Get all available books 
select *  from books
where availability = true;

-- Update Operation

-- make book false by using the bookid
update books 
set availability = false 
where bookid=4;
```

- update
```
-- make book false by using the bookid
update books 
set availability = false 
where bookid=4;

-- view changes 
select * from books;

-- Add new new to existing book
update books 
set genres = '{beauty}'
where bookid = 1



-- Add a borrowed book patron record
update patrons
set borrowed_books ='{4}'
where patronid =3;
-- View changes
select * from patrons;


```

- delete operation
```
delete from books
where title = 'Moby-Dick';

-- delete by id
delete from books
where bookid =1;
-- view changes 
select * from books;
```
