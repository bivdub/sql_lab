#SQL Lab


##Getting Started

To get started we'll need to import the booktown.sql file.

1. open terminal
2. use the command `psql -f booktown.sql`
3. type `sql` to open your psql console
4. type \list to ensure the booktown database was successfully completed

##Instructions
Provide the follow sql statements below each question.

##Order
1. Find all subjects sorted by subject
	SELECT * FROM subjects ORDER BY subject ASC;
2. Find all subjects sorted by location
	SELECT * FROM subjects ORDER BY location ASC;

##Where
1. Find the book "Little Women"
	SELECT * FROM books WHERE title = 'Little Women';
2. Find all books containing the word "Python"
	SELECT * FROM books WHERE title LIKE '%Python%';
3. Find all subjects with the location "Main St" sort them by subject
	SELECT * FROM subjects WHERE location = 'Main St' ORDER BY subject ASC;
##Joins

1. Find all books about Computers list ONLY book title
	SELECT books.title FROM books JOIN subjects ON subjects.id = books.subject_id WHERE subject LIKE '%Computers%';

* Find all books and display ONLY
	* Book title
	* Author's first name
	* Author's last name
	* Book subject

	SELECT books.title, authors.first_name, authors.last_name, subjects.subject FROM books JOIN subjects ON subjects.id = books.subject_id JOIN authors ON books.author_id = authors.id;

* Find all books that are listed in the stock table
	* Sort them by retail price (most expensive first)
	* Display ONLY: title and price

	SELECT stock.retail, books.title FROM stock JOIN editions ON stock.ISBN = editions.ISBN JOIN books ON editions.book_id = books.id ORDER BY stock.retail DESC;

* Find the book "Dune" and display ONLY
	* Book title
	* ISBN number
	* Publisher name
	* Retail price

	SELECT books.title, stock.isbn, publishers.name, stock.retail FROM books JOIN editions ON books.id = editions.book_id JOIN publishers ON editions.publisher_id = publishers.id JOIN stock ON editions.ISBN = stock.ISBN WHERE books.title = 'Dune';

* Find all shipments sorted by ship date display ONLY:
	* Customer first name
	* Customer last name
	* ship date
	* book title
	
	SELECT customers.first_name, customers.last_name, shipments.ship_date, books.title FROM shipments JOIN customers ON shipments.customer_id = customers.id JOIN editions ON shipments.isbn = editions.isbn JOIN books ON editions.book_id = books.id ORDER BY shipments.ship_date;

* Find all books that have either a 2nd or 3rd edition associated to it display ONLY:
	* Book title
	* Book Author
	* Edition Number

	SELECT books.title, authors.last_name, editions.edition FROM editions JOIN books ON books.id = editions.book_id JOIN authors ON books.author_id = authors.id WHERE editions.edition > 1;