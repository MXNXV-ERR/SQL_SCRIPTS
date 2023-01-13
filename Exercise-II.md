# *Exercise-II*

## Question

Consider the relations: PART, SUPPLIER and SUPPLY. The Supplier relation holds information<br>
about suppliers. The attributes SID, SNAME, SADDR describes the supplier. The Part relation holds<br>
the attributes such as PID, PNAME and PCOLOR. The Shipment relation holds information about<br>
shipments that include SID and PID attributes identifying the supplier of the shipment and the part<br>
shipped, respectively. The Shipment relation should contain information on the number of parts<br>
shipped.<br>
&ensp;a) Mention the constraints neatly.<br>
&ensp;b) Design the ER diagram for the problem statement<br>
&ensp;c) State the schema diagram for the ER diagram.<br>
&ensp;d) Create the above tables, insert suitable tuples and perform the following operations in<br>
&ensp;Oracle SQL:<br>
&emsp;1. Obtain the details of parts supplied by supplier #SNAME.<br>
&emsp;2. Obtain the Names of suppliers who supply #PNAME.<br>
&emsp;3. Delete the parts which are in #PCOLOR.<br>
&emsp;4. List the suppliers who supplies exactly two parts.<br>
&ensp;e) Create the table, insert suitable tuples and perform the following operations using<br>
&ensp;MongoDB<br>
&emsp;1. Update the details of parts for a given part identifier: #PID.<br>
&emsp;2. Display all suppliers who supply the part with part identifier: #PID.<br>
&emsp;3. Write a PL/SQL program to copy the contents of the Shipment table to another table<br>
&emsp;for maintaining records for specific part number.<br>


## d)Create the above tables, insert suitable tuples and perform the following operations in Oracle SQL:

### Creating the tables Part,supplier and supply

```sql
CREATE TABLE PART(
P_ID VARCHAR2(10) NOT NULL PRIMARY KEY,
P_NAME VARCHAR2(10),
P_COLOR CHAR(5));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q21.PNG?raw=True"></P>


```SQL
CREATE TABLE SUPPLIER(
S_ID VARCHAR2(10),
S_NAME VARCHAR2(10),
S_ADD VARCHAR2(20),
PRIMARY KEY(S_ID));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q22.PNG?raw=True"></P>


```SQL
CREATE TABLE SUPPLY(
S_ID VARCHAR2(10),
P_ID VARCHAR2(10),
QUANTITY NUMBER(3),
FOREIGN KEY(P_ID) REFERENCES PART(P_ID) ON DELETE CASCADE,
FOREIGN KEY(S_ID) REFERENCES SUPPLIER(S_ID) ON DELETE CASCADE,
PRIMARY KEY(S_ID,P_ID));
```

<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q23.PNG?raw=True"></P>


### Inserting values into the tables
```sql
INSERT INTO PART 
VALUES('&P_ID','&P_NAME','&P_COLOR');
 ```
 ```SQL
INSERT INTO SUPPLIER 
VALUES('&S_ID','&S_NAME','&S_ADD');
 ```
 ```SQL
INSERT INTO SUPPLY 
VALUES('&S_ID','&P_ID',&QUANTITY);
 ```

 <FIGURE>
<FIGCAPTION>PART</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q24.PNG?raw=True">
<FIGCAPTION>SUPPLIER</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q25.PNG?raw=True">
<FIGCAPTION>SUPPLY</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q26.PNG?raw=True">
</FIGURE>


### 1)Obtain the details of parts supplied by supplier #SNAME.

```SQL
SELECT * FROM PART
WHERE P_ID IN(SELECT P_ID FROM SUPPLY
              WHERE S_ID IN(SELECT S_ID FROM SUPPLIER
                            WHERE S_NAME = 'RAM'));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q2D1.PNG?raw=True"></P>


### 2)Obtain the Names of suppliers who supply #PNAME.

```sql
SELECT S_NAME FROM SUPPLIER
WHERE S_ID IN(SELECT S_ID FROM SUPPLY
              WHERE P_ID IN(SELECT P_ID FROM PART
     	                    WHERE P_NAME = 'BOLTS'));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q2D2.PNG?raw=True"></P>


### 3)Delete the parts which are in #PCOLOR.
```sql
DELETE FROM PART
WHERE P_COLOR = 'GREEN';
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q2D3.PNG?raw=True"></P>

<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q2D31.PNG?raw=True"></P>


### 4)List the suppliers who supplies exactly two parts.
```SQL
SELECT * 
FROM SUPPLIER
WHERE S_ID IN(SELECT S_ID
              FROM SUPPLY
              GROUP BY S_ID
              HAVING COUNT(P_ID)=2);
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q2D4.PNG?raw=True"></P>

## e) Create the table, insert suitable tuples and perform the following operations using MongoDB

Creating table in mongo
```javascript
db.createCollection("WAREHOUSE")
```

Inserting tuples in mongo
```javascript
db.WAREHOUSE.insert({"PNO":1947,"Pname":'bolts',"Colour":'Black',"SNO":1234,"Sname":'ABC',"Address":'blore'})
db.WAREHOUSE.insert({"PNO":2017,"Pname":'chain',"Colour":'Blue',"SNO":4567,"Sname":'DEF',"Address":'chen'})
db.WAREHOUSE.insert({"PNO":2017,"Pname":'chain',"Colour":'Blue',"SNO":3964,"Sname":'GHI',"Address":'mum'})
db.WAREHOUSE.insert({"PNO":1919,"Pname":'wheel',"Colour":'white',"SNO":4879,"Sname":'PQR',"Address":'delhi'})
db.WAREHOUSE.insert({"PNO":1956,"Pname":'nuts',"Colour":'black',"SNO":9988,"Sname":'STFU',"Address":'KOL'})
```

Inserted values
```javascript
db.WAREHOUSE.find().pretty()
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q2E0.PNG?raw=True"></P>
