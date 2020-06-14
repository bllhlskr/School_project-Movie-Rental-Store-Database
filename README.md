# School_project-Movie-Rental-Store-Database

<h3> E-R Diagram</h3>
<img src = 'img/E-R diagram.jpeg'>
<h3> Schema</h3>
<img src = 'img/schema database.jpeg'>

<h3>Report</h3>

We created this project, movie rental store database system, to make it easier for movie rental stores to categorize and keep track of the movies they rent, the movies’ properties (for example genre, condition, format), information and status data about the customers (name, address, e-mail) etc.

There is a database for all video stores, which keeps track of the stores’ names, address, phone and e-mail. There’s an ID for every store which is linked to all movies.

There’s also condition codes, genre type and format type for every movie. Condition code shows the condition of the movie (1 for new, 2 for good condition, 3 for damaged etc). There’s an ID and description for every movie genre (1 for horror, 2 for sci-fi etc) and and ID for every format (1 for CD, 2 for DVD etc).

The movies themselves also have other attributes. Those are movie title, release year, movie description, number of movies in stock, movie rent/sale status (is the movie for rent, for sale or both), daily rental rate and pricing.

Movie ID is linked to customer rentals. Customer rentals has attributes such as when the movie was taken, when it is returned or to be returned and the amount due. Customer rentals has 3 more things linked to it; rental status codes, financial transactions and customers. Rental status codes have 2 attributes which are rental status code and rental status description. Each code has a status description (1 for taken, 2 for returned etc).

Customers has 5 attributes; customer ID, first and last name, address and e-mail. Customer ID is linked to accounts. In accounts for each customer ID there’s an account ID, payment method code, account name and account details. Payment method code itself has payment method description (for example PayPal, credit card, cash etc).

Account ID is linked to Financial Transactions, which as previously mentioned is also linked to customer rentals. Financial transactions has attributes other than account ID such as transaction ID, item rental ID, previous transaction ID, transaction comment, transaction date and transaction amount. Transaction type code is linked to transaction type description, for example “payment completed” or “refunded”.
<br>
<h3> Queries to Create Tables</h3>
CREATE TABLE Movies(

Movie_id number(5) PRIMARY KEY,

Condition_code REFERENCES Condition_codes(condition_code), genre_type_id REFERENCES Genre_Types(genre_type_id), format_type_id REFERENCES Format_Types(format_type_id), store_id number(2) REFERENCES Video_Stores(store_id), movie_title varchar2(30) NOT NULL, release_year DATE DEFAULT (sysdate),

movie_description varchar2(999),

rental_or_sale_or_both varchar (6),

rental_daily_rate number(3) NOT NULL,

sale_price number(3));

CREATE TABLE Condition_Codes(

condition_code varchar2(15) PRIMARY KEY,

Condition_desc varchar2(100));

CREATE TABLE genre_types(

genre_type_id varchar2(15) PRIMARY KEY,

Genre_desc varchar2(300));

CREATE TABLE Format_Types(

format_type_id varchar2(15) PRIMARY KEY,

Format_type_desc varchar2(100));

CREATE TABLE Video_Stores(

store_id number(2) PRIMARY KEY,

store_name varchar2(15),

store_address varchar2(40),
 
store_phone varchar2(11),

store_email varchar2(20));





CREATE TABLE Customer_Rentals(

item_rental_id number(5) PRIMARY KEY ,

customer_id REFERENCES Customers(customer_id),

movie_id REFERENCES Movies(movie_id),

rental_status _code REFERENCES Rental_Status_Codes(rental_status_code), rental_date_out DATE DEFAULT (sysdate), rental_date_returned DATE DEFAULT (sysdate),

rental_amount_due number(3));

CREATE TABLE Rental_Status_Code(

Rental_status_code number(1),

Rental_status_desc varchar2(10));

CREATE TABLE Customers(

Customer_id number(7) PRIMARY KEY,

Customer_lname varchar2(25),

Customer_fname varchar2(25),

Customer_address varchar2(140),

Customer_email varchar2(40));

CREATE TABLE Accounts(

Account_id number(4) PRIMARY KEY,

Customer_id REFERENCES Customers(customer_id),

payment_method_code REFERENCES Payment_Methods(payment_method_code),

account_name varchar2(40),

account_details varchar2(100));

CREATE TABLE Payment_Methods(

Payment_method_code number(1) PRIMARY KEY
 
Payment_method_desc varchar2(20));



CREATE TABLE Financial_Transactions(

Transaction_id number(7) PRIMARY KEY,

item_rental_id REFERENCES Customer_Rentals(item_rental_id),

transaction_type_code REFERENCES Transaction_Types(transaction_type_code),

previous_transaction_id REFERENCES Transaction_Types(transaction_id),

transactin_comment varchar2(140),

transaction_date DATE DEFAULT (sysdate),

transaction_amount number(7));

CREATE TABLE Transaction_Types(

Transaction_type_code number(1));
<h3> Insert Into Statements</h3>
I Inserted 3 values for all tables.
<br>
INSERT INTO Movies VALUES (1, ‘box damaged,'Drama’,'Blu-ray’,3,'Joker’,2019,' In Gotham City, mentally troubled comedian Arthur Fleck is disregarded and mistreated by society. He then embarks on a downward spiral of revolution and bloody crime. This path brings him face-to-face with his alter-ego: the Joker’,25,'both’,12,3.99);

INSERT INTO Movies VALUES (2, ‘solid’,'Comedy’,'Blu-ray’,7,' Great Dictator’,1940,' The Great Dictator is a 1940 American political satire comedy-drama film written, directed, produced, scored by, and starring British comedian Charlie Chaplin’,12,'both’,17,6.99);

INSERT INTO Movies VALUES (3, ‘damaged’,'Sci-fi’,'Blu-ray’,2,'Transdence’,2014,' Synopsis. Dr. Will Caster (Johnny Depp) is a scientist who researches the nature of sentience, including artificial intelligence. He and his team work to create a sentient computer; he predicts that such a computer will create a technological singularity, or in his words Transcendence ’,37,'sale’,null,4.99);



INSERT INTO Condition_codes VALUES(‘box damaged’,'box is damaged but cd is fine’);

INSERT INTO Condition_codes VALUES(‘damaged’,'cd has skeches’ );

INSERT INTO Condition_codes VALUES(‘solid’,'everything is fine cd and box’);
 

INSERT INTO Genre_types VALUES(‘Comedy’, ‘A comedy film is a genre of film in which the main emphasis is on humor.’);

INSERT INTO Genre_types VALUES(‘Drama’, ‘Drama Films are serious presentations or stories with settings or life situations that portray realistic characters in conflict with either themselves, others, or forces of natüre.’);

INSERT INTO Genre_types VALUES(‘Sci-fi’, ‘Science fiction film is a genre that uses speculative, fictional science-based depictions of phenomena that are not fully accepted by mainstream science.’);



INSERT INTO Format_Types Values(‘Blu-ray’, ‘digital optical disc data storage format’);

INSERT INTO Format_Types Values(‘CD’, ‘ digital optical disc data storage format that was co-developed by Philips and Sony and released in 1982’);

INSERT INTO Format_Types Values(‘DVD’, ‘Stands for "Digital Versatile Disc. A dvd is a type of optical media used for storing digital data’);



INSERT INTO Video_stores VALUES(3,’Movie Madness 3’, ‘11280 Santa Monica Blvd, Los Angeles, CA 90025,

United States’, 1 310-312-8836,’store3 @ moviemadness.com’);

INSERT INTO Video_stores VALUES(7,’Movie Madness 7’, ‘4320 SE Belmont St, Portland, OR 97215, United

States’, 1 503-234-4363,’store7 @ moviemadness.com’);

INSERT INTO Video_stores VALUES(2,’Movie Madness 2’, ‘513 1st Ave N, Lewistown, MT 59457, United States’, 1 406-535-2100,’store7@moviemadness.com’);



INSERT INTO Customer_rentals VALUES(12458 , 3456987,1, 'rented’, TO_DATE ('05/19/2005', 'mm/dd/yyyy'), TO_DATE ('05/29/1997', 'mm/dd/yyyy'),2.99);

INSERT INTO Customer_rentals VALUES(23458 , 34574895,1, 'inStore’, null, null,null);

INSERT INTO Customer_rentals VALUES(12975 , 34589462,1, 'rented’, TO_DATE ('07/21/2005', 'mm/dd/yyyy'), TO_DATE ('07/28/2005', 'mm/dd/yyyy'),6.99);



INSERT INTO Customers VALUES(3456987, ‘Smith’,'John’, ‘ 7032 Lawrence Circle Caldwell, NJ 07006’,'John.Smith @ hotmail.com’);

INSERT INTO Customers VALUES(34574895 , ‘Griffin’,'Peter’, ‘ 7031 Spooner Street, ’PeterGriffin @ hotmail.com’);

INSERT INTO Customers VALUES(34589462 , ‘Soprano’,'Antony’, ‘ 67 Acacia Ave. Muncie, IN 47302 ’Tonysoprano @ hotmail.com’);
 
INSERT INTO Rental_Status_Codes VALUES(‘rented’, 'Its not in the store right now’);

INSERT INTO Rental_Status_Codes VALUES(‘inStore’, 'Its in the store right now’);

INSERT INTO Rental_Status_Codes VALUES(‘rented’, 'Its not in the store right now’);



INSERT INTO Accounts VALUES(2104, 34574895, 1 , ‘John Smith’,null);

INSERT INTO Accounts VALUES(2105, 34589462,2 , ‘Peter Griffin’,null);

INSERT INTO Accounts VALUES(2106, 3456987, 5 , ‘Tony Soprano’,null);





INSERT INTO Payment_Methods VALUES (1,'Cash’);

INSERT INTO Payment_Methods VALUES (2,’Amex’);

INSERT INTO Payment_Methods VALUES (5,'Paypal’);



INSERT INTO Financial_Transactions VALUES(2014789, 2104, 12458, 1 ,2014788,null, TO_DATE ('12/01/2006', 'mm/dd/yyyy'),20.00);

INSERT INTO Financial_Transactions VALUES(2014790, 2105, 23458, 2 ,2014789,’Refund to Peter Griffin’, TO_DATE ('12/01/2006', 'mm/dd/yyyy'),20.00);

INSERT INTO Financial_Transactions VALUES(2014791, 2106, 12975, 3 ,2014790,null, TO_DATE ('12/01/2006', 'mm/dd/yyyy'),20.00);



INSERT INTO Transaction_Types VALUES (1,'Payment’);

INSERT INTO Transaction_Types VALUES (2,'Refund’);

INSERT INTO Transaction_Types VALUES (3,'Debit’);
<br>
<h3>9 Different Queries To Test Database</h3>
<h4>Joins:</h4>

SELECT customer_id FROM Customers c, customer_rentals r

WHERE c.customer_id=r.customer_id; /* this statement returns customer id if its in both table*/
 


SELECT rental_status_code,movie_id FROM Customers c,Movies m

WHERE c.movie_id=m.movie_id; /* if both tabes have the same movie this statement returns their rental status code and movie id.*/



SELECT item_rental_id, transaction_date FROM Customer_Rentals c,Financial_Transactions f

WHERE c.item_rental_id = f.item_rental_id; /* if both tables have the same rental id this statement returns their item rental id and transaction date.*/



<h4>Nested Queries:</h4>

DELETE FROM Movies WHERE condition_code IN (SELECT condition_code FROM Condition_Codes WHERE condition_desc = ‘damaged’); /* this query deletes the damaged movies in movie table*/


UPDATE Movies SET sale_price = sale_price + 2.01 WHERE format_type_id IN (SELECT format_type_id FROM Format_types WHERE formattype_id = ‘DVD’); /* this query increase the price if the movie type is DVD*/


<h4>Set operations</h4>

SELECT * FROM Condition_codes

UNION

SELECT * FROM Genre_Types; /* This statement returns all the columns together in the conditions codes and genre types without duplicate rows*/



SELECT * FROM Rental_Status_Code

UNION ALL

SELECT * FROM Format_Types ; /* This statement returns all the columns together in the rental status code and format types with duplicate rows */





<h4>Aggregate Operations:</h4>

SELECT Count(customer_id) FROM Customers ;/* This returns customer number in the customer table.*/

SELECT AVG(sale_price) FROM Movie;/* This query returns average movie price in the stores.*/

