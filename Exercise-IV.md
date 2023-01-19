# *Exercise-IV*

## Question

Consider the Banking database – CUSTOMER, BRANCH, ACCOUNT and TRANSACTION. An<br>
account can be a savings account or a current account. Customer can have both types of accounts.<br>
The transactions can be a deposit or a withdrawal. Mention the constraints neatly.<br>
&ensp;a) Design the ER diagram for the problem statement<br>
&ensp;b) State the schema diagram for the ER diagram.<br>
&ensp;c) Create the above tables, insert suitable tuples and perform the following operations in<br>
&ensp;SQL:<br>
&emsp;1. Obtain the details of customers who have both Savings and Current Account.<br>
&emsp;2. Retrieve the details of branches and the number of accounts in each branch.<br>
&emsp;3. Obtain the details of customers who have performed at least 3 transactions.<br>
&emsp;4. List the details of branches where the number of accounts is less than the average<br>
&emsp;number of accounts in all branches.<br>
&ensp;d) Create the table, insert suitable tuples and perform the following operations using<br>
&ensp;MongoDB<br>
&emsp;1. Find the branch name for a given Branch_ID.<br>
&emsp;2. List the total number of accounts for each customer.<br>
&ensp;e) Using cursors demonstrate the process of copying the contents of one table to a new table.<br>

## c)Create the above tables, insert suitable tuples and perform the following operations in SQL:

### Creating the tables Customer,Branch,Account,Transaction

```sql
CREATE TABLE CUSTOMER( 
    CID VARCHAR2(10) NOT NULL PRIMARY KEY, 
    NAME VARCHAR2(10), 
    PHNO NUMBER(10));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q41.PNG?raw=True"></P>

```SQL
CREATE TABLE BRANCH (
    BID VARCHAR2(10) NOT NULL PRIMARY KEY, 
    BLOC VARCHAR2(20));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q42.PNG?raw=True"></P>

```SQL
CREATE TABLE ACCOUNT( 
    CID VARCHAR2(20) REFERENCES CUSTOMER(CID), 
    ACCNO NUMBER(12) NOT NULL PRIMARY KEY, 
    BAL NUMBER(7), 
    TYPE VARCHAR2(10), 
    BID VARCHAR2(10) REFERENCES BRANCH(BID));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q43.png?raw=True"></P>

```sql
CREATE TABLE TRANSACTION( 
CID VARCHAR2(10) REFERENCES CUSTOMER(CID), 
TID VARCHAR2(20) NOT NULL PRIMARY KEY, 
ACCNO NUMBER(12) REFERENCES ACCOUNT(ACCNO), 
AMT NUMBER(7), 
TTYPE VARCHAR2(10));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q44.png?raw=True"></P>

### Inserting values into the tables
```SQL
INSERT INTO CUSTOMER 
VALUES('&CID','&NAME',&PHNO); 
```
```SQL
INSERT INTO BRANCH 
VALUES('&BID','&BLOC');
```
```SQL
INSERT INTO ACCOUNT 
VALUES('&CID',&ACCNO,&BAL,'&TYPE','&BID'); 
```
```SQL
INSERT INTO TRANSACTION 
VALUES('&CID','&TID',&ACCNO,&AMT,'&TTYPE');
```
 <FIGURE>
<FIGCAPTION>CUSTOMER</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q45.png?raw=True">
<FIGCAPTION>BRANCH</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q46.png?raw=True">
<FIGCAPTION>ACCOUNT</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q47.png?raw=True">
<FIGCAPTION>TRANSACTION</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q48.png?raw=True">
</FIGURE>


### 1. Obtain the details of customers who have both Savings and Current Account.
hUMM buLL aDVise :Be cArEfUl Of ThE cASe oR wAsTe tIme fINdinG tHE eRRor😎
```SQL
SELECT * FROM CUSTOMER
WHERE CID IN (
    SELECT CID FROM ACCOUNT WHERE TYPE='SA'
)
AND CID IN (
     SELECT CID FROM ACCOUNT WHERE TYPE='CA'
);
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q4D1.PNG?raw=True"></P>

### 2.Retrieve the details of branches and the number of accounts in each branch.
```SQL
SELECT B.BID,BLOC,COUNT(ACCNO) 
FROM ACCOUNT A JOIN BRANCH B ON A.BID=B.BID
GROUP BY B.BID,BLOC;
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q4D1.PNG?raw=True"></P>

### 3.Obtain the details of customers who have performed at least 3 transactions.
```SQL
SELECT * 
FROM CUSTOMER
WHERE CID IN(SELECT CID 
             FROM TRANSACTION 
             GROUP BY CID 
             HAVING COUNT(TID)>=3);
```

### 4.List the details of branches where the number of accounts is less than the average number of accounts in all branches.
```SQL
SELECT B.BID,BLOC,COUNT(ACCNO) 
FROM ACCOUNT A JOIN BRANCH B ON A.BID=B.BID
GROUP BY B.BID,BLOC
HAVING COUNT(ACCNO)<(SELECT AVG(TEMP.COU) 
                     FROM (SELECT COUNT(ACCNO) AS COU 
                           FROM ACCOUNT GROUP BY BID)TEMP);
```
-OR-
```SQL
SELECT B.BID,BLOC,COUNT(ACCNO) 
FROM ACCOUNT A JOIN BRANCH B ON A.BID=B.BID
GROUP BY B.BID,BLOC
HAVING COUNT(ACCNO)<(SELECT AVG(COUNT(ACCNO)) 
                           FROM ACCOUNT GROUP BY BID);
```

## d)Create the table, insert suitable tuples and perform the following operations using MongoDB