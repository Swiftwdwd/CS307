# Lecture 2
## SQL
```SQL
select column_name
from table_name
where condition
```
### TWO main components
* Data Definition Language(DDL): CREATE, ALTER, DROP
* Data Manipulation Language(DML): INSERT, UPDATE, DELETE, SELECT
## Create table
Some classic rules
* Table (and column) names must be start with a letter (PostgreSQL tolerates an underscore_) and only contain letters, digits, or underscores.
* The $ sign is also accepred, and some products allow #.
Datatypes
* Text
```SQL
char(fixed-size length) --char = char(1)
varchar(max length)
varchar2(max length) --ORACLE
clob --Gb
```
* Number
```SQL
int
float
numeric(precision, scale) --numeric(8, 2) 999999.99
```
* Date
```SQL
date --includes time, down to second with Oracle, not with other products
datetime --down to second (other than Oracle, DB2 and PostgreSQL)
timestamp --down to 0.000001 second, Replace datetime in DB2/PostgreSQL
```
* Binary
```SQL
raw(max length)
varbinary(max length)
blob, bytea
--RAW in Oracle, and VARBINARY (SQL Server) are the binary equivalent of VARCHAR.
--BLOB is the binary equivalent of CLOB (BLOB means Binary Large Object).
--PostgreSQL calls the binary datatype BYTEA.
```
create a table
```SQL
create table people ( peopleid   int,
                      first_name varchar(30),
                      surname    varchar(30),
                      born       numeric(4),
                      died       numeric(4))   
```
* null means nothing, notset.
```SQL
create table people ( peopleid   int not null,
                      first_name varchar(30),
                      surname    varchar(30) not null, --column people.surname is 'Surname or stage name'
                      born       numeric(4) not null,
                      died       numeric(4))   
```
## Constraints
Constraints are declarative rules that the DBMS will check every time new data will be added, when data is changed, or even when data is deleted, in order to prevent any inconsistency. Any operation that violates a constraint fails and returns an error.
* NOT NULL is a constraint. But thereare many others. For instance, PRIMARY KEY tells which is the main key for the table, and indicates two thing:
  * that the value is mandatory (the additional NOT NULL doesn't hurt but is redundant), and
  * that the values are unique (no duplicates allowed in the column)
```SQL
create table people ( peopleid   int not null
                                 primary key,
                      first_name varchar(30)
                check (first_name = upper(first_name)),
                      surname    varchar(30) not null
                check (surname = upper(surname)),
                      born       numeric(4) not null,
                      died       numeric(4),
                      unique (first_name, surname)) --The first name and surname are unique in the table.
```
* referential integrity
```SQL
create table movies (movieid        int not null primary,
                     title          varchar(60) not null,
                     country        char(2) not null,
                     year_released  numeric(4) not null
                                 check (year_released >= 1895),
                     unique (title, country, year_released)
                      foreign key(country)
                               references countries(country_code))
```
