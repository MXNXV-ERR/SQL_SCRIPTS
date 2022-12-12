# *Exercise-V*

## Question

Consider the Book Lending system from the library- BOOKS, STUDENT, BORROWS. The
students are allowed to borrow any number of books on a given date from the library. The details of
the book should include ISBN, Title of the Book, author and publisher. All students need not
compulsorily borrow books.
&ensp;a) Mention the constraints neatly.<br>
&ensp;b) Design the ER diagram for the problem statement<br>
&ensp;c) State the schema diagram for the ER diagram.<br>
&ensp;d) Create the above tables, insert suitable tuples and perform the following operations in<br>
&ensp;SQL:<br>
&ensp;1. Obtain the names of the student who has borrowed either book bearing ISBN ‘123’<br>
&ensp;or ISBN ‘124’.<br>
&ensp;2. Obtain the Names of female students who have borrowed “Database” books.<br>
&ensp;3. Find the number of books borrowed by each student. Display the student details<br>
&ensp;along with the number of books.<br>
&ensp;4. List the books that begin with the letters “DA” and has never been borrowed by any<br>
&ensp;students.<br>
&ensp;e) Create the table, insert suitable tuples and perform the following operations using<br>
&ensp;MongoDB<br>
&ensp;1. Obtain the book details authored by “author_name”.<br>
&ensp;2. Obtain the Names of students who have borrowed “Database” books.<br>
&ensp;f) Write a PL/SQL procedure to print the first 8 Fibonacci numbers and a program to call<br>
&ensp;the same.<br>

## a)Mention the constraints neatly.
- PRIMARY KEY CONSTRAINT
    - STUDENTS : USN
    - BOOKS : ISBN
    - BORROWS : ISBN,USN
- REFRENTIAL CONSTRAINTS
    - BORROWS USN REFERENCES STUDENTS USN
    - BORROWS ISBN REFRENCES BOOKS ISBN


## d) Create the above tables, insert suitable tuples and perform the following operations in SQL:
### Creating entities books,student,borrows
```SQL
CREATE TABLE BOOKS(
ISBN VARCHAR2(20),
TITLE VARCHAR2(20),
AUTHOR CHAR(20),
PUBLISHER VARCHAR2(20),
PRIMARY KEY(ISBN));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q51.png?raw=True"></P>

```SQL
CREATE TABLE STUDENTS(
USN VARCHAR2(10) NOT NULL PRIMARY KEY,
NAME CHAR(20),
SEMESTER INT,
DEPARTMENT VARCHAR2(10),
GENDER CHAR(1));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q52.png?raw=True"></P>

```SQL
CREATE TABLE BORROWS( 
ISBN VARCHAR2(20), 
USN VARCHAR2(10), 
DATEBORROWED DATE, 
FOREIGN KEY(USN) REFERENCES STUDENTS(USN), 
FOREIGN KEY(ISBN) REFERENCES BOOKS(ISBN), 
PRIMARY KEY(ISBN,USN));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q53.png?raw=True"></P>

### Inserting values into the tables

```SQL
INSERT INTO BOOKS 
VALUES('&ISBN','&TITLE','&AURTHOR','&PUBLISHER');
```
```SQL
INSERT INTO STUDENTS
VALUES('&USN','&NAME','&SEMESTER','&DEPARTMENT','&GENDER');
```
```SQL
INSERT INTO BORROWS
VALUES('&ISBN','&USN','&DATEBORROWED');
```
<FIGURE>
<FIGCAPTION>BOOKS</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q54.png?raw=True">
<FIGCAPTION>STUDENTS</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q55.png?raw=True">
<FIGCAPTION>BORROWS</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q56.png?raw=True">
</FIGURE>

### 1)Obtain the names of the student who has borrowed either book bearing ISBN ‘123’ or ISBN ‘124’
Changed query according according to my input
```sql
SELECT NAME FROM STUDENTS
WHERE USN IN(SELECT USN FROM BORROWS
             WHERE ISBN='ISB123' OR ISBN='ISB554');
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q5D1.png?raw=True"></P>

### 2)Obtain the Names of female students who have borrowed “Database” books.
```SQL
SELECT NAME
FROM STUDENTS
WHERE USN IN(SELECT USN 
             FROM  BORROWS
             WHERE ISBN IN(SELECT ISBN 
                           FROM BOOKS
                           WHERE TITLE='DATABASE')) AND GENDER='F';
```

<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q5D2.png?raw=True"></P>

### 3)Find the number of books borrowed by each student. Display the student details along with the number of books.
```SQL
SELECT B.USN,NAME,COUNT(ISBN)
FROM BORROWS B,STUDENTS S
WHERE S.USN=B.USN
GROUP BY B.USN,NAME;
```

<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q5D3.png?raw=True"></P>

### 4) List the books that begin with the letters “DA” and has never been borrowed by any students.
```sql
SELECT *
FROM BOOKS 
WHERE TITLE LIKE 'DA%' AND ISBN NOT IN(SELECT ISBN
                                       FROM BORROWS);
```

## e) Create the table, insert suitable tuples and perform the following operations using MongoDB

Creating table in mongo
```javascript
db.createCollection("Books")
```

Inserting tuples in mongo
```javascript
db.Books.insert({"ISBN":"B123","Title":"Database","Author":"Ramu","Publisher":"Sharma","borrowed_by":"Student":"Owais","USN":"IS081","Dept":"ISE"}})
db.Books.insert({"ISBN":"B124","Title":"Cloud","Author":"Rakesh","Publisher":"Verma","borrowed_by":"Student":"Maitri","USN":"CS067","Dept":"CSE"}})
db.Books.insert({"ISBN":"B125","Title":"Database","Author":"Ramu","Publisher":"Sharma","borrowed_by":"Student":"Jeevika","USN":"IS055","Dept":"ISE"}})
db.Books.insert({"ISBN":"B126","Title":"MC","Author":"Ravi","Publisher":"Cengage","borrowed_by":"Student":"Prajwal","USN":"CS085","Dept":"CSE"}})
```

To view contents
```javascript
db.Books.find().pretty()
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q5E0.png?raw=True"></P>

### 1)Obtain the book details authored by “author_name”.
```javascript 
db.Books.find({"Author":"Ramu"}).pretty()
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q5E1.png?raw=True"></P>

### 2)Obtain the Names of students who have borrowed “Database” books
``` javascript
db.Books.find({"Title":"Database"},{"borrowed_by.Student":1})
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q5E2.png?raw=True"></P>



## f) Write a PL/SQL procedure to print the first 8 Fibonacci numbers and a program to call the same.

```SQL
SQL>CREATE OR REPLACE PROCEDURE FIBONACCI(N IN NUMBER)
...IS
...A NUMBER;
...B NUMBER;
...C NUMBER;
...I NUMBER;
...BEGIN
...     A:=0; B:=1;
...    DBMS_OUTPUT.PUT_LINE(A);
...    DBMS_OUTPUT.PUT_LINE(B);
...    FOR I IN 1..N-2 LOOP
...        C:=A+B;
...        DBMS_OUTPUT.PUT_LINE(C);
...        A:=B;
...        B:=C;
...    END LOOP;
...END FIBONACCI;
```


```sql
EXEC FIBONACCI(8)
```


ELSE PROGRAM

```SQL
DECLARE
    N NUMBER:=&N;
BEGIN
    EXEC FIBONACCI(N);
END;
/
```