                                                                                SQL
SQL is structured(fixed data model or fixed schema) query langiage use to communicate between the user  and data 
SQL commands-
1. DDL - The DDL Commands are used to create and modify the schema of the database and its objects. The commands of Data Definition Language deal with how the data should exist in the database.

-DDL  (Data definition languge)
{
	Create -(create box(table))
	alter(change structure)
	Drop (remove structure)
	truncate (remove data from structure)
	rename (rename the structure)
}

2. DML(Data Manipulate Language)

DML is use to manipulate the data of the table, such as insert into the table ,delete from the table and update from the table etc.
after creating structure for performing retrive, delete, update, insert we use DML commands.

DML (Data manipulation language)
{
	Select 
	Insert 
	Update
	Delete
}

Who user can fetch the data we give them grant means which types of grant we have to give
like he can view or insert or delete update etc.

3. DCL - DCL includes commands such as GRANT and REVOKE which mainly deal with the rights, permissions, and other controls of the database system. 
-DCL (Data Control Language)
{
	Grant
	Revoke

}
4. TCL() - It use to manage the transaction of the database like commit ,rollback,savepoint etc.

-TCL (Transation Control Language)
{
	Commit (commit is use to save the manipulated  changes permanently.)
	Roll Back (roll back is use to undo the transation.)
	Save Point (savepoint is a point of transation where we can check the transaction back.)
}

## Constrains
{
	Primary Key
	foreign key
	Check
	Unique
	Default
	Not Null
}

------------------------------------


# DDL
----1. create----

create table TABLE_NAME
(
	column1_name datatype,
	column2_name datatype,
	column3_name datatype
);

desc table_name - To see the schema of the table.

create table emp(
	id int,
	name varchar(2),
	salary number(10)
);
desc emp;

-----2. Alter----------

change something in schems(structure)


Student
  int   varchar
  | id | name |
  |	   |      |
 
 if we want to insert a new clm name address then

alter table Student add address varchar(20);

eg-
create table employee(
	id int,
	name varchar(10)
	);
desc employee;

add a column name address
alter table employee add address varchar(10);


drop a column
alter table employee drop column address;


modefy datatype
alter table employee modify id varchar(10); //previously id was intger now it is charactor.

change column name from id to roll_no
alter table employee rename column id to roll_no;

change table name
alter table employee rename to emplo 

desc employee //object does not exist
desc emplo



-------------------Constrains in sql-------------------------------------

Constrains means condition- we want to add some conditions so that in that way user should perform operations
we will apply condition based on column(attribute col ka hi naam h)

1. Unique - if we apply unique in collum then collum have not any duplicate value.

2. Not NUll- for collum that is not empty that contain some value ,when we apply this in out query that will give some value for paticular collum.

3. Primary key - (Unique + Not NULL) - For Example for employee has unique id and we have to give that id each employee.

4. Check - we want to fix some domain value.
   when user will enter the which will satisfy the check condittion then only it will allow to enter the data in to table.
   Example - check age > 10 user > 10 ;

5. Foreign key- (referential integrity) - Foreign key refers to primery key of the tables .it link two tables together as we put data across many table to minimize the redundancy,
   foreign key also maintain referential intergrity.

6. Default - By default it will take default given value in to the column.
   Example - Salary int default 10000;


------------------------------Aggrigate functions in Sql-------------------------------


emp
    |  e_id   |   e_name   |  dept   |  salary  |
    |		  |			   |         |          |
    |	1	  |	  Ram	   |   HR    |  10000   |
    |	2	  |	  Asis	   |   MRKT  |  20000   |
    |	3	  |	  Ravi	   |   HR    |  30000   |
    |	4	  |	  Nitin	   |   MRKT  |  40000   |
    |	5	  |	  varun    |   IT    |  50000   |
    |	6	  |	  Sunday   | Testing |  Null    | //null means not avilable, does not mean 0


Aggrigate functions in Sql  
Max, Min, Count, Avg, Sum

1.Max - it will find the maximum value of the paticular column.
Example

find maximum salary from emp table .
   select Max(salary) from emp;  // Output-50000

2.Min - it will find the minimum value of the particular column.
Example-find minimum salary from emp table.
   select min(salary) from emp;  //Output-10000  

3.Count - It will count the total number of value of the column. 

    select count(*) from emp;  //6  total 6 rows are there in table
	select count(salary) from emp; //5 null will not be counted.
	select Distinct(count(salary)) from emp;  //4 unique values from salary ka count.

4.Avg - It will give the average value of numeric column.
Example-find avg of salary   
	   select Avg(salary) from emp;  // output - 10000  
	   avg=sum(salary)/count(ssalary)

5.Sum - This function  return the total sum of numeric column.
Example - select sum(salary) from emp;  //1,40,000  total sum of salary
	select distinct(sum(salary)) from emp;  // it will suming up the uniquely .


------------------------------JOINS in Sql-------------------------------


A SQL Join statement is used to combine data or rows from two or more tables based on a common field between them. Different types of Joins are:
1.INNER JOIN
2.LEFT JOIN
3.RIGHT JOIN
4.FULL JOIN

                         Student
	|    ROLL_NO  |   NAME   |   ADDRESS  |  PHONE |  AGE |
	|       1     |   SHIVAM |    DELHI   |  XXXXX |  18  |
	|       2     |   SAKSHMA|    BHOPAL  |  XXXXX |  19  |
	|       3     |   DEEP   |    KOLKATA |  XXXXX |  18  |
	|       7     |   ROHIT  |    MUMBAI  |  XXXXX |  18  |
	|       8     |   NIRAJ  |    ALIPUR  |  XXXXX |  20  |

	        StudentCourse
	| COURSE-ID  |   ROLL-NO  |
	|     1      |     1      |
	|     2      |     2      |
	|     2      |     3      |
	|     3      |     4      |
	|     1      |     5      |
	|     4      |     9      |


### 1. INNER JOIN: 
The INNER JOIN keyword selects all rows from both the tables as long as the condition satisfies. 

Syntax:

   FROM table1 
   INNER JOIN table2
   ON table1.matching_column = table2.matching_column;

table1: First table.
table2: Second table

matching_column: Column common to both the tables.


following query shows the names and age of students enrolled in different courses.


SELECT StudentCourse.COURSE_ID, Student.NAME, Student.AGE FROM Student
INNER JOIN StudentCourse
ON Student.ROLL_NO = StudentCourse.ROLL_NO;

output:

| COURSE-ID |  NAME   |  AGE  |
|   1       | SHIVAM  |  18   |
|   2       | SAKSHAM |  19   |
|   2       | KALYAN  |  20   |
|   3       |  DEEP   |  18   |

### 2. LEFT JOIN: 
Left join returns all the rows of the table on the left side of the join and matching rows for the table on the right side of join. 


SYNTAX :

    FROM table1 
    LEFT JOIN table2
    ON table1.matching_column = table2.matching_column;





    table1: First table.

    table2: Second table

    matching_column: Column common to both the tables.


SELECT Student.NAME,StudentCourse.COURSE_ID 
FROM Student
LEFT JOIN StudentCourse 
ON StudentCourse.ROLL_NO = Student.ROLL_NO;

OUTPUT: 
     |   NAME   |  COURSE-ID  |
	 |  SHIVAM  |     1       |
	 |  SAKSHAM |     2       |
	 |  KALYAN  |     2       |
	 |  DEEP    |     3       |


### 3. RIGHT JOIN: 
RIGHT JOIN is similar to LEFT JOIN. This join returns all the rows of the table on the right side of the join and matching rows for the table on the left side of join. 

SYNTAX:

FROM table1 
RIGHT JOIN table2
ON table1.matching_column = table2.matching_column;





table1: First table.
table2: Second table

matching_column: Column common to both the tables.


SELECT Student.NAME,StudentCourse.COURSE_ID 
FROM Student
RIGHT JOIN StudentCourse 
ON StudentCourse.ROLL_NO = Student.ROLL_NO;

OUTPUT:

|   NAME   |   COURSE-ID  |
|  SHIVAM  |      1       |
|  SAKSHAM |      2       |
|  PRATEEK |      2       |
|  KALYAN  |      2       |
|   DEEP   |      3       |



### 4. FULL JOIN: 

FULL JOIN creates the result-set by combining result of both LEFT JOIN and RIGHT JOIN. The result-set will contain all the rows from both the tables. 
The rows for which there is no matching, the result-set will contain NULL values.

SYNTAX:

FROM table1 
FULL JOIN table2
ON table1.matching_column = table2.matching_column;





table1: First table.
table2: Second table


matching_column: Column common to both the tables.

SELECT Student.NAME,StudentCourse.COURSE_ID 
FROM Student
FULL JOIN StudentCourse 
ON StudentCourse.ROLL_NO = Student.ROLL_NO;

OUTPUT:

| NAME  |   COURSE-ID |
| ROHIT |     NULL    |
| SHIVAM|      1      |
| NIRAJ |     NULL    |
| NULL  |      9      |
| NULL  |      10     |
| RIYANK|       2     |




