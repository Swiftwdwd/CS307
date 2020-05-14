# Lecture 3
## Select
```SQL
select * from tablename -- In programs, do not use *.
```
* where
  * number
  * 'constant' If not ', it will be as a column.
  * column
```SQL
select * from movies
where country = 'us'
```
* two select
```SQL
select *
from (select * from movies
      where country = 'us') us_movies
where year_released between 1940 and 1949
```
```SQL
select *
from (select * from movies
      where year_released between 1940 and 1949) movies_from_the_1940s
where country = 'us'
```
The two speed are different.
* and
```SQL
select *
from movies
where country = 'us'
  and year_released between 1940 and 1949
```
* or (and > or)
* not
* =
* <> or !=
* < <=
  * 2 < 10 true
  * '2' < '10' false
  * '2-JUN-1883' > ' 1-DEC-2056' also compare string not date
* > >=
* in
```SQL
where (country = 'us'
       or country = 'gb')
  and year_released between 1940 and 1949
  
where country in ('us', 'gb')
  and year_released between 1940 and 1949
```
```SQL
where country not in ('us, 'gb')
```
* like
  * % any character (include 0)
  * _ only 1 character
```SQL
select * from movies
where title not like '%A%'
  and title not like '%a%'
  
where upper(title) not like '%A%' -- Not good to apply a function to a searched column
```
## Date
* European DD/MM/YYYY
* American MM/DD/YYYY
* China YYYY/MM/DD
```SQL
select * from forum_posts where post_date >= '2018-03-12'; -- it's ok but prefer the following.
select * from forum_posts where post_date >= date('2018-03-12');
select * from forum_posts where post_date >= date('12 March, 2018');
```
* date and datetime
  * date default 00:00:00
```SQL
year_released between 1940 and 1949 -- we can not change 1940 and 1949
is shorthand for this:
year_released >= 1940 and year_released <= 1949
```
## NULL
* NULL in SQL is NOT a value.
```SQL
where column_name = null -- false. NULL is just NULL
where column_name is null -- ok
where column_name is not null -- ok
## Some Functions
```SQL
select title, year_released -- column
from movies
where country = 'us'
```
* databases
  * schemas
    * tables
      * columns
    * desc movies; Oracle/MySQL
* concatenating
  * 'hello' || 'world' DB2/Oracle/PostgreSQL/SQLite
  * 'hello' + 'world' SQLServer
  * concat('hello', 'world') MySQL
```SQL
select title
       || ' was released in '
       || year_released movie_release -- column name
from movies
where country = 'us'
```
```SQL
select title
       || ' was released in '
       || cast(year_released as varchar) movie_release -- year_released is int, better convert to varchar
from movies
where country = 'us'
```
```SQL
select peopleod, surname,
  date_part('year', now())-born as age -- now() is current time, take out year of current time
from people
where died is null
```
```SQL
select f(column1), ...
from some_table
where f(some_column) = f(some_user_input) -- f(some_column) is not good
```
* round(3.1415, 3)  3.142
* trunc(3.1415, 3)  3.141 directly three bit
* upper(), lower()
* substr('Citizen Kane', 5, 3)  'zen'
* trim(' Oops ')  'Oops'  only delete space in the beginning and end
* replace('Sheep', 'ee', 'i')  'Ship'
* cast
```SQL
select cast(born as char)||'abc' from people;
select cast(born as char(2))||'abc' from people;
select cast(born as char(10))||'abc' from people;
select cast(born as varchar)||'abc' from people;
select cast(born as varchar(2))||'abc' from people;
```
## Case
```SQL
case upper(color)  -- color is column name
  when 'Y' then 'Color' 
  when 'N' then 'B&W'
  else '?' -- null is here
end as color
```
```SQL
case column_name
  when null then -- false
  else ...
end
```
find someone's status
```SQL
case
  when died is null then
        'alive and kicking'
  else 'passed away'
end as status
```
```SQL
select surname,
  case
    when died is null then
          'alive and kicking'
    else 'passed away'
  end as status
from people
```
