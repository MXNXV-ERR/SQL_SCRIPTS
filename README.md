# Click on below links for complete solution of each excercise
* [Excercise-I (3 TABLES)](https://github.com/MXNXV-ERR/dbmslab/blob/main/Exercise-I.md)<BR>
* [Excercise-I (4 TABLES)(Recommended)](https://github.com/MXNXV-ERR/dbmslab/blob/main/Exercise-I(NEW).md)<BR>
* [Excercise-III](https://github.com/MXNXV-ERR/dbmslab/blob/main/Exercise-III.md)<br>
* [Excercise-V](https://github.com/MXNXV-ERR/dbmslab/blob/main/Exercise-V.md)<br>


# SQL_SCRIPTS

## CREATE:
      USED TO CREATE A NEW EMPTY TABLE
      
**SYNTAX:**
      
```sql
create table tablename(attr1 datatype1,attr2 datatype 2......);
```
      
 EXAMPLE:
 ```sql
      create table student(
      usn varchar2(20) not null primary key,
      name char(20),
      age number(10),
      gender char(3));
 ```

## INSERT:
      USED TO INSERT NEW TUPLES OR VALUES INTO THE TABLE
      
 **SYNTAX:**
 ```sql
 insert into tablename values(value1,value2,......);
 ```
  EXAMPLE:
      REFERING TO INSERT THERE ARE TWO KINDS OF METHODS TO ENTER THE VALUES.

   TYPE1:
   ```sql
      insert into student values('1MS20IS090','KRISHNA',19,'M');
   ```
   TYPE2:
   ```sql
      insert into student values('&usn','&name',&age,&gender);
      enter the value for usn:1MS20IS090
      enter the value for name:KRISHNA
      enter the vakue for age:19
      enter the value for gender:M
   ```
## DESCRIPTION:
      USED TO KNOW THE DESCRIPTION OF THE TABLE
      
   **SYNTAX:**
   ```sql
      desc table tablename;
   ```
   EXAMPLE:
   ```sql
      desc table student;
   ```
## SELECT:
      USED TO RETRIEVE THE REQUIRED COLUMN VALUES FROM THE TABLE
      
   **SYNTAX:**
   ```sql
      select column names from tablename;
   ```
   EXAMPLE:
      HERE TOO WE HAVE TWO KINDS

   TYPE1:
    SELECT THE REQUIRED COLUMNS.
   ```sql
      select name,usn from student;
   ```
   TYPE2:
    SELECT EVERY COLUMN FROM THE TABLE.
   ```sql
      select * from student;
   ```
## DELETE:
      USED TO DELETE AN EXISTING TUPLE FROM THE TABLE
      
   **SYNTAX:**
   ```sql
      delete from tablename where condition;
   ```
   EXAMPLE:
   ```sql
      delete from student 
      where usn='1MS20IS090';
   ```
      HERE WHERE CLAUSE IS USED TO DENOTE WHICH TUPLE WE ARE ACTUALLY ASKING THE COMPILER TO DELETE.
      
## DROP:
      USED TO DROP AN ENTIRE TABLE FROM THE DATABASE
      
   **SYNTAX:**
   ```sql
      drop table tablename;
   ``` 
   EXAMPLE:
   ```sql
      drop table student;
   ```
## ALTER:
      USED TO ALTER THE ATTRIBUTES OF THE TABLE.ALTER USES SOME KEYWORDS TO ALTER THE TABLE.
      i) ADD: to add a new attribute to the existing table
      ii) MODIFY: to modify the already existing attribute.
      
   **SYNTAX:**
   ```sql
      alter table tablename add/modify column_name datatype;
   ``` 
   EXAMPLE:
   ```sql
      1. alter table student
         add dept_id varchar2(20);
      2. alter table student
         modify usn number(10);
   ```
## UPDATE:
      USED TO UPDATE THE ROWS OR THE TUPLES
      
   **SYNTAX:**
   ```sql
      update tablename
      set col1=val1,col2=val2......
      where condition;
   ```
   EXAMPLE:
   ```sql
      update student
      set name='KRISHNA;
      where usn='1MS20IS090';
   ```
      
      
