# *Exercise-III*

## Question

Consider the relations BOAT, SAILOR and RESERVES. The relation BOAT identifies the features<br>
of a boat such as unique identifier, color and a name. The list of sailors with attributes such as<br>
SailorID, name, age etc., are stored in the relation SAILOR. The sailors are allowed to reserve any<br>
number of boats on any day of the week and the records are to be updated in the RESERVES table.<br>
&ensp;a) Mention the constraints neatly.<br>
&ensp;b) Design the ER diagram for the problem statement<br>
&ensp;c) State the schema diagram for the ER diagram.<br>
&ensp;d) Create the tables, insert suitable tuples and perform the following operations in SQL:<br>
&emsp;1. Obtain the details of the boats reserved by ‘#Sailor_Name’.<br>
&emsp;2. Retrieve the BID of the boats reserved necessarily by all the sailors.<br>
&emsp;3. Find the number of boats reserved by each sailor. Display the Sailor_Name along<br>
&emsp;with the number of boats reserved.<br>
&emsp;4. Identify which boats have the same name as their sailor.<br>
&ensp;e) Create the table, insert suitable tuples and perform the following operations using<br>
&emsp;MongoDB.<br>
&emsp;1. Obtain the number of boats obtained by sailor :#Sailor_Name<br>
&emsp;2. Retrieve boats of color :”#color”<br>
&ensp;f) Write a PL/SQL program to check whether a given number is prime or not.<br>


## a)Mention the constraints neatly.
- PRIMARY KEY CONSTRAINT
    - SAILOR: SAILOR_ID
    - BOAT : BOAT_ID
    - RESERVES : SAILOR_ID,BOAT_ID
- REFRENTIAL CONSTRAINTS
    - RESERVES SAILOR REFERENCES SAILOR SAILOR_ID
    - RESERVES BOAT_ID REFERENCES BOAT BOAT_ID

## d)Create the tables, insert suitable tuples and perform the following operations in SQL:
### Creating entities boat,sailor,reserves
```SQL
CREATE TABLE BOAT(
BOAT_ID VARCHAR2(20),
BOAT_NAME CHAR(20),
BOT_COLOR CHAR(10),
PRIMARY KEY(BOAT_ID));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q31.png?raw=True"></P>

```SQL
CREATE TABLE SAILOR(
SAILOR_ID VARCHAR2(20),
SAILORNAME CHAR(20),
AGE NUMBER(3),
RATING VARCHAR(9),
PRIMARY KEY(SAILOR_ID));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q32.png?raw=True"></P>

```SQL
CREATE TABLE RESERVES(
BOAT_ID VARCHAR2(20) REFERENCES BOAT(BOAT_ID),
SAILOR_ID VARCHAR2(20) REFERENCES SAILOR(SAILOR_ID),
DAY CHAR(10),
PRIMARY KEY(BOAT_ID,SAILOR_ID));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q33.png?raw=True"></P>

### Inserting values into the tables
```SQL
INSERT INTO BOAT
VALUES('&BOAT_ID','&BOAT_NAME','&BOAT_COLOR');
```
```SQL
INSERT INTO SAILOR
VALUES('&SAILOR_ID','&SAILORNAME',&AGE,'&RATING');
```
```SQL
INSERT INTO RESERVES
VALUES('&BOAT_ID','&SAILOR_ID','&DAY');
```
<FIGURE>
<FIGCAPTION>BOAT</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q34.png?raw=True">
<FIGCAPTION>SAILOR</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q35.png?raw=True">
<FIGCAPTION>RESERVES</FIGCAPTION>
<IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q36.png?raw=True">
</FIGURE>


### 1) Obtain the details of the boats reserved by ‘#Sailor_Name’.
```SQL
SELECT *
FROM BOAT
WHERE BOAT_ID IN(SELECT BOAT_ID
                 FROM RESERVES
                 WHERE SAILOR_ID IN (SELECT SAILOR_ID
                                     FROM SAILOR
                                     WHERE SAILORNAME='MANAV'));
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q3D1.png?raw=True"></P>

### 2) Retrieve the BID of the boats reserved necessarily by all the sailors
```SQL
SELECT BOAT_NAME,BOAT_ID
FROM BOAT B
WHERE NOT EXISTS (SELECT *
                  FROM SAILOR S
                  WHERE NOT EXISTS (SELECT * 
                                    FROM RESERVES R
                                    WHERE R.SAILOR_ID=S.SAILOR_ID AND R.BOAT_ID=B.BOAT_ID)) ;
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q3D2.png?raw=True"></P>


### 3)Find the number of boats reserved by each sailor. Display the Sailor_Name along with the number of boats reserved.
```SQL
SELECT SAILORNAME,COUNT(R.BOAT_ID)
FROM RESERVES R ,SAILOR S
WHERE R.SAILOR_ID=S.SAILOR_ID
GROUP BY SAILORNAME;
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q3D3.png?raw=True"></P>

### 4)Identify which boats have the same name as their sailor.
```SQL
SELECT BOAT_NAME,SAILORNAME
FROM BOAT B JOIN SAILOR S
ON B.BOAT_NAME=S.SAILORNAME;
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q3D4.png?raw=True"></P>

## e)Create the table, insert suitable tuples and perform the following operations using MongoDB.
Creating table in mongo
```javascript
db.createCollection("BOATRES")
```
Inserting tuples in mongo
```javascript
db.BOATRES.insert({"BID":9988,"BNAME":'ABC',"COLOUR":'Black',"SNAME":'John',"SID":1234,"DAY":'2017-12-25'})
db.BOATRES.insert({"BID":8877,"BNAME":'DEF',"COLOUR":'Black',"SNAME":'Smith',"SID":4567,"DAY":'2017-11-24'})
db.BOATRES.insert({"BID":7766,"BNAME":'GHI',"COLOUR":'Blue',"SNAME":'Sucre',"SID":1122,"DAY":'2017-10-24'})
db.BOATRES.insert({"BID":6655,"BNAME":'PQR',"COLOUR":'white',"SNAME":'Sucre',"SID":1122,"DAY":'2017-10-29'})
```
To view contents
```javascript
db.Employee.find().pretty()
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q3E0.png?raw=True"></P>

### 1)Obtain the number of boats obtained by sailor :#Sailor_Name
```javascript
db.BOATRES.find({"SNAME":'Sucre'}).count()
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q3E1.png?raw=True"></P>

### 2)Retrieve boats of color :”#color”
```javascript
db.BOATRES.find({"COLOUR":'Black'}).pretty()
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q3E2.png?raw=True"></P>

### f) Write a PL/SQL program to check whether a given number is prime or not.

```SQL
DECLARE
    N NUMBER :=&N;
    J NUMBER :=2;
    FLAG NUMBER :=0;
BEGIN
    WHILE J<=N/2 LOOP
        IF MOD(N,J)=0 THEN
            DBMS_OUTPUT.PUT_LINE(N||' IS NOT A PRIME NUMBER');
            FLAG:=1;
            EXIT;
        ELSE
            J:=J+1;
        END IF;
    END LOOP;
    IF FLAG=0 THEN
        DBMS_OUTPUT.PUT_LINE(N||' IS A PRIME NUMBER');
    END IF;
END;
/
```
<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q3F1.png?raw=True"></P>

<P ALIGN="CENTER"><IMG SRC="https://github.com/MXNXV-ERR/SQL_SCRIPTS/blob/main/IMGS/Q3F2.png?raw=True"></P>
