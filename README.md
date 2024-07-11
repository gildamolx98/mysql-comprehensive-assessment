# mysql-comprehensive-assessment
/*Topic : Library Management System
You are going to build a project based on Library Management System. It keeps track of all information about books
 in the library, their cost, status and total number of books available in the library.

Create a database named library and following TABLES in the database: 

1. Branch 
2. Employee 
3. Books
4. Customer
5. IssueStatus
6. ReturnStatus 

Attributes for the tables: 

1. Branch
• Branch_no
Set as PRIMARY KEY  
• Manager_Id  
• Branch_address  
• Contact_no 

2. Employee  
• Emp_Id – Set as PRIMARY KEY  
• Emp_name  
• Position  
• Salary
• Branch_no
Set as FOREIGN KEY and it refer Branch_no in Branch table  

3. Books  
• ISBN
Set as PRIMARY KEY  
• Book_title  
• Category  
• Rental_Price  
• Status [Give yes if book available and no if book not available]  
• Author  
• Publisher

4. Customer  
• Customer_Id
Set as PRIMARY KEY  
• Customer_name  
• Customer_address  
• Reg_date 

5. IssueStatus  
• Issue_Id – Set as FOREIGN KEY and it refer customer_id in CUSTOMER table 
Set as PRIMARY KEY  
• Issued_cust 
. Issued_book_name 
• Issue_date 
• Isbn_book – Set as FOREIGN KEY and it should refer isbn in BOOKS table 

6. ReturnStatus  
• Return_Id
Set as PRIMARY KEY  
• Return_cust  
• Return_book_name  
• Return_date  
• Isbn_book2
Set as FOREIGN KEY and it should refer isbn in BOOKS table */

create database library ;
use library ;

create table branch(Branch_no int PRIMARY KEY,  
 Manager_Id int, 
Branch_address  varchar (30)
,Contact_no int);
desc branch;
INSERT INTO Branch (Branch_no, Manager_Id, Branch_address, Contact_no)
VALUES
  (1, 101, 'Address 1', 11151111),
  (2, 102, 'Address 2', 345678901),
  (3, 103, 'Address 3', 34567890),
  (4, 104, 'Address 4', 45678123),
  (5, 105, 'Address 5', 678901234),
  (6, 106, 'Address 6', 89012345),
  (7, 107, 'Address 7', 890123456),
  (8, 108, 'Address 8', 901234567),
  (9, 109, 'Address 9', 901234678),
  (10, 110, 'Address 10',12345678);
select * from branch ;

create table Employee(Emp_Id int PRIMARY KEY  , Emp_name  varchar (20)
,Position varchar(20) ,Salary int,Branch_no int,FOREIGN KEY (Branch_no) REFERENCES branch(branch_no));
desc employee ;
INSERT INTO Employee (Emp_Id, Emp_name, Position, Salary, Branch_no)VALUES
  (1001, 'John Don', 'Manager', 60000, 1),
  (1002, 'Janu Smitha', 'Assistant', 30000, 2),
  (1003, 'Robi Johnson', 'Librarian', 40000, 3),
  (1004, 'Alice Abraham', 'Assistant', 30000, 4),
  (1005, 'Mickel Dany', 'Librarian', 40000, 5),
  (1006, 'Emily Shanker', 'Assistant', 30000, 6),
  (1007, 'David Luka', 'Librarian', 40000, 7),
  (1008, 'Sara Tasni', 'Assistant', 30000, 8),
  (1009, 'Kevin bosco', 'Librarian', 40000, 9),
  (1010, 'Lisa Nijas', 'Assistant', 30000, 10);
select * from employee ;

create table Books(ISBN int PRIMARY KEY,Book_title  varchar(30),Category  varchar(20),
Rental_Price  int,Status char(3), Author  varchar(20),Publisher varchar(30));
desc books ;
INSERT INTO Books (ISBN, Book_title, Category, Rental_Price, Status, Author, Publisher)VALUES
(10001,'Accounting Principles','Finance',2168,'yes','Wiley','DBooks'),
(10002,'Cost Management','Accounting',1703,'yes','McGraw-Hill','Deakon_stall'),
(10003,'Accounting Systems','Accounting',2012,'no','McGraw-Hill','B-4_books'),
(10004,'Individual Taxation','finance', 2517,'yes','Pearson','Bold_books'),
(10005,'Intermediate Accounting','Finance',3421,'no','Wiley','don_books'),
(10006,'Advanced Accounting',' Accounting',784,'yes','klingston','peek_books'),
(10007,'Swimming life','sports',2356,'yes','Smith','BudgetBooks'),
(10008,'Cricket is my life','biography',414,'no','Davies','Universal'),
(10009,'Physical state','theory',1098,'yes','Chan','TechBooks'),
(10010,'Athlet in cancer','story',425,'no','Smitha','BudgetBooks');
select * from books;


create table  Customer(Customer_Id int PRIMARY KEY ,Customer_name  varchar(20),
Customer_address varchar(30), Reg_date date);
desc customer;
insert into customer(customer_id,customer_name,customer_address,reg_date)values
(51,'sijo','qwe house','2012-03-19'),
(52,'gini','rty house','2017-9-20'),
(53,'hima','asd home','2022-3-2'),
(54,'joni','zxc home','2024-5-8'),
(55,'fina','dfg home','2024-2-17'),
(56,'kevin','lkj home','2014-9-19'),
(57,'lima','dig home','2018-1-19'),
(58,'tina','yut home','2017-1-20'),
(59,'jina','bvh home','2018-9-22'),
(60,'sanu','gyt home','2014-3-24');
select * from customer;

create table IssueStatus(Issue_Id int PRIMARY KEY , Issued_cust varchar(20), Issued_book_name varchar(30),
Issue_date date,Isbn_book int ,FOREIGN KEY(issue_id) REFERENCES CUSTOMER(customer_id) ,FOREIGN KEY(Isbn_book) references books(isbn)); 
desc issuestatus;
insert into issuestatus(issue_id,issued_cust,issued_book_name,issue_date,isbn_book) values
(51,'sijo','Accounting Principles','2019-6-5',10001),
(58,'tina','Swimming life','2018-09-22',10007),
(56,'joni','Physical state','2024-5-8',10009),
(52,'gini','Individual Taxation','2022-3-2',10004),
(53,'hima','Accounting Principles','2024-3-5',10001),
(55,'fina','Swimming life','2024-09-22',10007),
(54,'joni','Physical state','2024-5-8',10009),
(57,'lima','coat management','2022-03-2',10002),
(59,'jina','Physical state','2023-5-8',10009),
(60,'sanu','Swimming life','2024-05-22',10007);
select * from issuestatus ;

create table ReturnStatus(Return_Id int PRIMARY KEY  ,Return_cust varchar(20),Return_book_name  varchar(30),Return_date date, 
Isbn_book2 int,FOREIGN KEY(isbn_book2) references books(isbn));
desc ReturnStatus;
insert into returnstatus(return_id,return_cust,return_book_name,return_date,isbn_book2)values
(501,'joni','Physical state','2024-11-8',10009),
(502,'jina','Physical state','2024-5-8',10009),
(503,'sanu','Swimming life','2024-06-22',10007),
(504,'sijo','Accounting Principles','2020-6-5',10001),
(505,'gini','Individual Taxation','2024-3-2',10004),
(506,'fina','Swimming life','2024-10-22',10007),
(507,'hima','Accounting Principles','2024-7-5',10001),
(508,'tina','Swimming life','2018-09-22',10007),
(509,'joni','Physical state','2024-6-8',10009),
(510,'lima','coat management','202-012-2',10002);
select * from returnstatus;

-- Display all the tables and Write the queries for the following :

-- 1. Retrieve the book title, category, and rental price of all available books. 

select book_title,category,rental_price from books where status = 'yes';

-- 2. List the employee names and their respective salaries in descending order of salary. 

select emp_name,salary from employee order by salary desc ;

-- 3. Retrieve the book titles and the corresponding customers who have issued those books. 

select b.book_title ,i.issued_cust from books b join issuestatus i where isbn = isbn_book ;

-- 4. Display the total count of books in each category. 

select category,count(category) 'total count of books in each category' from books group by category ;

-- 5. Retrieve the employee names and their positions for the employees whose salaries are above Rs.50,000. 

select emp_name,position from employee where salary > 50000 ;

-- 6. List the customer names who registered before 2022-01-01 and have not issued any books yet. 

select customer_name from customer where reg_date < '2022-01-01' and Customer_name not in (select Issued_cust from IssueStatus); 

-- 7. Display the branch numbers and the total count of employees in each branch. 

select branch_no,count(branch_no) 'total employee in each branch' from employee group by branch_no ;

-- 8. Display the names of customers who have issued books in the month of march 2022.

select issued_cust from issuestatus where issue_date between '2022-03-01' and '2022-03-31' ; 

-- 9. Retrieve book_title from book table containing accounting. 

select book_title from books where category = 'accounting' ;

-- 10.Retrieve the branch numbers along with the count of employees for branches having more than 5 employees

select branch_no ,count(branch_no) from employee group by branch_no having count(*) > 5 ; -- 'no branches contain more than 5 employees'.

-- 11. Retrieve the names of employees who manage branches and their respective branch addresses.

select e.emp_name,b.branch_no,b.branch_address from employee e left join branch b on e.branch_no=b.branch_no where position ='manager';

-- 12.  Display the names of customers who have issued books with a rental price higher than Rs. 2000.

select i.issued_cust ,b.book_title,b.rental_price from issuestatus i left join books b on i.isbn_book = b.isbn where rental_price > 2000;
