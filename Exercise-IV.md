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
CREATE TABLE BRANCH(
B_NO NUMBER(5) NOT NULL PRIMARY KEY,
ADDR VARCHAR2(20));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q41.PNG?raw=True"></P>

```SQL
CREATE TABLE ACCOUNT( 
ACC_NO NUMBER(12) NOT NULL PRIMARY KEY, 
BALANCE NUMBER(15), 
TYPE VARCHAR(20));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q42.PNG?raw=True"></P>

```SQL
CREATE TABLE CUSTOMER( 
C_ID NUMBER(10) NOT NULL PRIMARY KEY, 
NAME CHAR(10), 
PH_NO NUMBER(10), 
B_NO NUMBER(5) REFERENCES BRANCH(B_NO) ON DELETE CASCADE, 
ACC_NO NUMBER(12) REFERENCES ACCOUNT(ACC_NO) ON DELETE CASCADE);
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q43.png?raw=True"></P>

```sql
CREATE TABLE TRANSACTION( 
ACC_NO NUMBER(12) REFERENCES ACCOUNT(ACC_NO) ON DELETE CASCADE, 
AMOUNT NUMBER(15), 
TRANS_TYPE VARCHAR(20), 
TRANS_ID NUMBER(20) NOT NULL PRIMARY KEY);
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q44.png?raw=True"></P>

### Inserting values into the tables
```SQL
INSERT INTO BRANCH 
VALUES(&B_NO,'&ADDR'); 
```
```SQL
INSERT INTO ACCOUNT 
VALUES(&ACC_NO,&BALANCE,'&TYPE');
```
```SQL
INSERT INTO CUSTOMER 
VALUES(&C_ID,'&NAME',&PH_NO,&B_NO,&ACC_NO); 
```
```SQL
INSERT INTO TRANSACTION 
VALUES(&ACC_NO,&AMOUNT,'&TRANS_TYPE',&TRANS_ID);
```
 <FIGURE>
<FIGCAPTION>BRANCH</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q45.png?raw=True">
<FIGCAPTION>ACCOUNT</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q46.png?raw=True">
<FIGCAPTION>CUSTOMER</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q47.png?raw=True">
<FIGCAPTION>TRANSACTION</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q48.png?raw=True">
</FIGURE>


### 1. Obtain the details of customers who have both Savings and Current Account.
hUMM buLL aDVise :Be cArEfUl Of ThE cASe oR wAsTe tIme fINdinG tHE eRRor😎
```SQL
SELECT * FROM CUSTOMER
WHERE C_ID IN(SELECT C_ID FROM ACCOUNT
              WHERE TYPE='savings'
              INTERSECT
              SELECT C_ID FROM ACCOUNT
              WHERE TYPE='current');
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q4D1.PNG?raw=True"></P>
