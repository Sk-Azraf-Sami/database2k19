## Installation process
> 1) Download the ([Oracle 11g Express edition](https://www.oracle.com/database/technologies/xe-prior-release-downloads.html)) and install the software.
> 2) Remember the password during the installation because this password is used for connecting the database account.

![alt text](https://github.com/shahidul034/BookList_database-project/blob/master/DIAGRAM%20PIC/installation.png)

> 3) Open the SQL Plus. Write 'connect system' and use the password that you set in the installation process. Follow the below figure.

![alt text](https://github.com/shahidul034/database-project/blob/master/DIAGRAM%20PIC/sqlplus.png)

> 4) You can create a new user because we use the system(administrator) as a user. Then, we will give the new user all privileges to perform all SQL tasks. Follow the figure.
```
create user shakib034 identified by shakib034;
grant all privileges to shakib034;
```
![alt text](https://github.com/shahidul034/database-project/blob/master/DIAGRAM%20PIC/sqlplus2.png)
## Database project demo
| ![](https://github.com/shahidul034/database-project/blob/master/DIAGRAM%20PIC/pic1.png) | 
|:--:| 
| *SCHEMA* |
<!-- ![alt text](https://github.com/shahidul034/database-project/blob/master/DIAGRAM%20PIC/pic1.png) -->
<!-- ![alt text](https://github.com/shahidul034/database-project/blob/master/DIAGRAM%20PIC/p3.png) -->
| ![](https://github.com/shahidul034/database-project/blob/master/DIAGRAM%20PIC/P4.png) | 
|:--:| 
| *ERD* |
<!-- ![alt text](https://github.com/shahidul034/database-project/blob/master/DIAGRAM%20PIC/P4.png) -->
<!-- ![alt text](https://github.com/shahidul034/database-project/blob/master/DIAGRAM%20PIC/p2.png) -->
## Run the SQL command
> You can run SQL script by using the SQL command line. Besides, you can write your SQL command in a txt file and save the txt file as a SQL extension. Then, type the below command in the SQL command line.
```
start C:\Users\andromeda\Desktop\file.sql
```
## Oracle data types
Here is a link about the [oracle data types.](https://www.w3resource.com/oracle/oracle-data-types.php)
## Checking current user name
```
show user
```
## Checking the existing table in database.
```
select table_name from user_tables;
```

![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/show_table_name.png)

> It shows that we already have two tables in my database. So we need to drop those tables from the database for a fresh start. You can use this command to drop any table.
```
drop table department;
drop table course;
```
> First, we create the table "dept". Here, we can see that the primary key is dept_id because it uniquely identifies each row in the table.
```
Create table dept(
dept_id number(20),
dept_name varchar(30),
faculty varchar(30),
no_of_student number(20),
primary key(dept_id)
);
```
> We also create a course, book and relation table.
```
Create table course(
course_no varchar(20),
course_name varchar(50),
year_semister number(3),
credit number(20,4),
dept_id number(20),
primary key(course_no),
foreign key(dept_id) references dept(dept_id)
);
create table book(
book_no number(20),
book_name varchar(50),
author varchar(50),
book_edition number(4),
course_offering number(6),
primary key(book_no) 
);
create table relation(
book_no number(20),
course_no varchar(20),
primary key(book_no,course_no),
foreign key (book_no) references book(book_no),
foreign key (course_no) references course(course_no) 
);
```
> When you observe the course table, they have another foreign key keyword referencing the dept_id from the "dept" table. We insert something in the course table. We must check whether this dept_id exists in the "dept" table.

# DDL
## Add column in the table
> We add a column in the dept table which is location.
> 
> Command structure: alter table **table_name** add **column_name** **column_definition**;
```
alter table dept add location char(20);
```
## Modify column definition in the table
> Command structure: alter table **table_name** modify **column_name** **column_definition**;
> 
> We modify the location data types char(20) to varchar(23);
```
alter table dept modify location varchar(23);
```
## Rename the column name
> Command structure: alter table **table_name** rename **column_name** to **column_name**;
```
alter table dept rename column location to location2;
```
## Drop the column from table
> Command structure: alter table **table_name** drop column **column_name**;
```
alter table dept drop column location2;
```
# DML
## Insert the data in our table
```
insert into dept(dept_id,dept_name,faculty,no_of_student)values(7,'CSE','EE',120);
```
> Here, "dept" refers to the table name, and we also insert values according to table columns.
> We also insert values into the other tables.

## Insert the data in the table
```
insert into dept(dept_id,dept_name,faculty,no_of_student)values(7,'CSE','EE',120);
insert into dept(dept_id,dept_name,faculty,no_of_student)values(3,'EEE','EE',120);
insert into dept(dept_id,dept_name,faculty,no_of_student)values(1,'CE','CE',120);
insert into dept(dept_id,dept_name,faculty,no_of_student)values(5,'ME','ME',120);
insert into dept(dept_id,dept_name,faculty,no_of_student)values(2,'ECE','EE',60);

insert into course(course_no,course_name,year_semister,credit,dept_id)values('CSE1101','discreate math',11,3.00,7);
insert into course(course_no,course_name,year_semister,credit,dept_id)values('CSE3105','database systems',31,3.00,7);
insert into course(course_no,course_name,year_semister,credit,dept_id)values('EEE1101','Basic electrical engineering',11,3.00,3);
insert into course(course_no,course_name,year_semister,credit,dept_id)values('ME3101','solid mechanics',31,3.00,5);

insert into book(book_no,book_name,author,book_edition,course_offering)values(12,'discreate math','rosen',4,2);
insert into book(book_no,book_name,author,book_edition,course_offering)values(13,'database systems','korth',5,1);
insert into book(book_no,book_name,author,book_edition,course_offering)values(14,'data_communication','willim stallings',6,3);
insert into book(book_no,book_name,author,book_edition,course_offering)values(15,'solid mechanics','john abraham',3,2);
insert into book(book_no,book_name,author,book_edition,course_offering)values(16,'electrical engineering','boylsted',8,4);

insert into relation(book_no,course_no)values(12,'CSE1101');
insert into relation(book_no,course_no)values(16,'EEE1101');
insert into relation(book_no,course_no)values(15,'ME3101');
insert into relation(book_no,course_no)values(13,'CSE3105');

```
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/dept_table.png)
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/course_table.png)
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/book_table.png)
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/relation_table.png)
> All the data are inserted. Now, we do some experiments here. We run the command below.

```
insert into course(course_no,course_name,year_semister,credit,dept_id)values('MME1101','Basic structure of materials',11,3.00,9);
```
> We inserted the course_no "MME1101" and course_id "9" in the course table. After running the command, we found this error.
> The course table refers to the dept table, and course id "9" does not exist in the dept table. So, it shows this error.

![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/error.png)
## Displaying table data using SELECT command
> Now, we find the rows from the "dept" table, which have 120 students using the select command.

```
select * from dept where no_of_student=120;
```
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/select.png)

> We find the dept_name, which course name is "database systems".
```
select * from dept where dept_id=(select dept_id from course where course_name='database systems');
```
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/subquery.png)

> Here, we add extra select command by adding an additional condition to find the dept_id in the "dept" table. This type of query is called a subquery.

## Updating the data in a table
> Now we want to update the value of the course name from the course table where course_no is "EEE1101";
> Command structure: update table_name set column_name=value where condition;
```
update course set course_name='Digital Electronics' where course_no='EEE1101';
```
## Deleting row from a table
> We add an extra row to perform the delete operation in the dept table.
```
insert into dept(dept_id,dept_name,faculty,no_of_student)values(12,'URP','CE',60);
```
> Now we delete the row from the dept table where dept_id is 12.

> Command structure: delete from  **table_name** where **condition**;
```
delete from  dept where dept_id=12;
```
## union, intersect, and except
```
select dept_name from dept where dept_name like 'E%' union select dept_name from dept where dept_name like '%M%';
```
# Save the SQL command output
## Save the SQL command output in csv file
> Simply change the folder path and your sql command.
```
SET MARKUP XML ON
SET HEADING OFF
SET PAGESIZE 0
SET FEEDBACK OFF
SPOOL C:\Users\andromeda\Desktop\file.csv
SELECT *
FROM dept;
SPOOL OFF
```
## Save the SQL command output in xml file
> Simply change the folder path and your sql command.
```
SET COLSEP ","
SET HEADING OFF
SET PAGESIZE 0
SET FEEDBACK OFF
SPOOL C:\Users\andromeda\Desktop\file.csv
SELECT *
FROM dept;
SPOOL OFF
```
## Save the SQL command output in txt file
> Simply change the folder path and your sql command.
```
SPOOL C:\Users\andromeda\Desktop\file.txt
SELECT *
FROM dept;
SPOOL OFF
```
## Aggregate function
We count how many row exist in dept table.
```
select count(*) from dept;
 ```
 We also give alias name to any output in select command.
 ```
select count(dept_name) as number_of_dept from dept;
 ```
We can count distinct department name in dept table.
 ```
select count(distinct dept_name) as number_of_dept from dept;
 ```
We can count average and total no. of students in dept table.
 ```
select avg(no_of_student) from dept;
select sum(no_of_student) from dept;
 ```
We can find max and min no. of students of any department from dept table.
 ```
 select max(no_of_student) from dept;
 select min(no_of_student) from dept;
```
## Group by and Having
> Find the average of student according to faculty.
```
select faculty,avg(no_of_student) from dept group by faculty;

```
![alt text](https://github.com/shahidul034/BookList_database-project/blob/master/DIAGRAM%20PIC/group%20by.png)

> Find the average of student according to faculty where average of student is greater than 60. 
 ```
 select faculty,avg(no_of_student) from dept group by faculty having avg(no_of_student)>60;
 ```
 ![alt text](https://github.com/shahidul034/BookList_database-project/blob/master/DIAGRAM%20PIC/having.png)
 
 ## Nested subquery
 > Find the department name where the “rosen”(author) book is taught.
```
 select dept_name from dept where dept_id=(select dept_id from course where course_no=(select course_no from relation where book_no=(select book_no from book where author='rosen')));
```
 ![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/subquery2.png)
## Set Membership(AND, OR,NOT)
Find the rows where faculty is "EE" and "CSE" string exists in course_no.
```
select * from dept where faculty='EE' and dept_id in (select dept_id from course where course_no like '%CSE%')
```
## some/all/exists/unique
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/some.png)
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/all.png)
```
select * from book where book_no> some(select book_no from book where book_no>=14);
select * from book where book_no> all(select book_no from book where book_no>=14);
```
The exists construct returns the value true if the argument subquery is nonempty.
```
select * from course where year_semister>=11 and exists(select * from dept where faculty like '%EE%');
```
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/exist.png)

## String operations
> percent ( % ).  The % character matches any substring.

> underscore ( _ ).  The _ character matches any character.

> Demo table.

![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/table_test.png)

> 'E%' matches any string beginning with “E”.

```SELECT * FROM TEST WHERE NAME LIKE 'E%';```

![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/begin.png)

> '%E' matches any string ending with “E”.
> 
```SELECT * FROM TEST WHERE NAME LIKE '%E';```

![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/end.png)

> '%E%E%' contains with 'EE'.

```SELECT * FROM TEST WHERE NAME LIKE '%E%E%';```

> '_ _ _' matches any string of exactly three characters.

```
SELECT * FROM TEST WHERE NAME LIKE '___';
```

>  Below command matches any string of at least three characters and at most five characters.


```SELECT * FROM TEST WHERE NAME LIKE '___' or NAME LIKE '____' or NAME LIKE '_____';```

## Join operations

```
select * from dept natural join course where dept_id=7;
```
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/natural_join_with_conditon.png)
```
select * from dept natural join course;
```
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/natural_join.png)

```
select dept_name,course_name from dept join course using(dept_id);
select dept_name,course_name from dept join course on dept.dept_id=course.dept_id;
```
![alt text](https://github.com/shahidul034/database2k19/blob/main/DIAGRAM%20PIC/join.png)

```
select dept_name,course_name from dept left outer join course using(dept_id);
select dept_name,course_name from dept right outer join course using(dept_id);
select dept_name,course_name from dept full outer join course using(dept_id);
select dept_name,course_name from dept left outer join course on dept.dept_id=course.dept_id;
```
## Views
View definition is not the same as creating a new relation by evaluating the query expression.

A view of dept without their faculty,no_of_student.
```
create view dept_details as select dept_id,dept_name from dept;

```
Find all course in the CSE department.
```
create view CSE_DEPT_COURSE as select course_name from course where dept_id=(select dept_id from dept where dept_name='CSE');
```
Views Defined Using Other Views
```
create view  custom as select * from dept_details where dept_id>=3;
```
## Cascading Actions in Referential Integrity
```
Create table course2(
course_no varchar(20),
course_name varchar(50),
year_semister number(3),
credit number(20,4),
dept_id number(20),
primary key(course_no),
foreign key(dept_id) references dept(dept_id)
on delete cascade
);
insert into dept2(dept_id,dept_name,faculty,no_of_student)values(7,'CSE','EE',120);
insert into dept2(dept_id,dept_name,faculty,no_of_student)values(3,'EEE','EE',120);
insert into dept2(dept_id,dept_name,faculty,no_of_student)values(1,'CE','CE',120);
insert into dept2(dept_id,dept_name,faculty,no_of_student)values(5,'ME','ME',120);
insert into dept2(dept_id,dept_name,faculty,no_of_student)values(2,'ECE','EE',60);

insert into course2(course_no,course_name,year_semister,credit,dept_id)values('CSE1101','discreate math',11,3.00,7);
insert into course2(course_no,course_name,year_semister,credit,dept_id)values('CSE3105','database systems',31,3.00,7);
insert into course2(course_no,course_name,year_semister,credit,dept_id)values('EEE1101','Basic electrical engineering',11,3.00,3);
insert into course2(course_no,course_name,year_semister,credit,dept_id)values('ME3101','solid mechanics',31,3.00,5);
```

```
delete from dept2 where dept_id=5;
```
## Set line size and page size
```
set pagesize 100
set linesize 200
```
