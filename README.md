# School_project-Movie-Renta-Store-Database
<h1>Movie Rental Store Database</h1>
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
