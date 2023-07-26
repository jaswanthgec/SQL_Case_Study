# SQL_Case_Study
case study about creating database for a healthcare organisaition and a database for library management system
SQL Case study required code for creating tables of Patients:

//for creating a patient table

CREATE TABLE `test`.`patient_table` (
 `Name` VARCHAR(45) NOT NULL,
 `Address` VARCHAR(100) NOT NULL,
 `Date_of_Birth` VARCHAR(45) NOT NULL,
 `Contact_Details` VARCHAR(12) NOT NULL,
 PRIMARY KEY (`Name`),
 UNIQUE INDEX `Contact_Details_UNIQUE` (`Contact_Details` ASC) VISIBLE);

//for creating a medical history table

CREATE TABLE `test`.`medical_history_table` (
 `Diagnoses_Yes_Or_No` VARCHAR(10) NOT NULL,
 `Treatements` VARCHAR(10) NOT NULL,
 `Surgeries` VARCHAR(10) NOT NULL,
 `Medication` VARCHAR(10) NOT NULL,
 PRIMARY KEY (`Diagnoses_Yes_Or_No`));

//for creating a lab result table

CREATE TABLE `test`.`lab_result_table` (
 `Blood_Test` VARCHAR(10) NOT NULL,
 `Urine_Test` VARCHAR(10) NOT NULL,
 `Imaging_Test` VARCHAR(10) NOT NULL);

//for creating a prescription table

CREATE TABLE `test`.`prescription_table` (
 `Medicine_Name` VARCHAR(45) NOT NULL,
 `Dosage` VARCHAR(45) NOT NULL,
 `Frequency` VARCHAR(45) NOT NULL,
 PRIMARY KEY (`Medicine_Name`));

//for creating a out come table

CREATE TABLE `test`.`out_come_table` (
 `Read_Mission_Rates` INT NOT NULL,
 `Medication_Adherence` VARCHAR(45) NOT NULL,
 PRIMARY KEY (`Read_Mission_Rates`));


Creating tables for Library Management System

//for creating book table

create table book_table(book_id int,title varchar(20),author varchar(20),publisher varchar(20),publication_year date,isbn int,genre varchar(10),availability boolean,primary key(book_id));

//for creating borrowers table

create table borrowers_table(borrower_id int,name varchar(30),address varchar(50),phone_number numeric,email varchar(20),primary key(borrower_id));

//for creating loans table

create table loans_table(loan_id int,book_id int,borrower_id int,date_borrowed date,due_date date,date_returned date,foreign key(book_id) references book_table(book_id),foreign key(borrower_id) references borrowers_table(borrower_id),PRIMARY key(loan_id));

//for creating reservation table

create table reservations_table(reservation_id int,book_id int,borrower_id int,date_reserved date,date_needed date,status varchar(10),primary key(reservation_id), foreign key(book_id) references book_table(book_id),foreign key(borrower_id) references borrowers_table(borrower_id));

QUERYING THE DATABASE:

SELECT FROM book_table WHERE availability = 1;

Get all borrowed books:

SELECT book_table.title, book_table.author, borrowers_table.name, loans_table.dateborrowed, loans_table.due_date
FROM Books
INNER JOIN Loans ON book_table.book_id = loans_table.book_id
INNER JOIN Borrowers ON loans_table.borrower_id = borrowers_table.borrower_id;

Get all reserved books:

SELECT book_table.title, book_table.author, borrowers_table.name, reservations_table.date_reserved,
Reservations_table.date_needed
FROM book_table
INNER JOIN reservations_table ON book_table.book_id = reservations_table.book_id;

