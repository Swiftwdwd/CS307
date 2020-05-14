# Lecture 4
## Distinct
```SQL
select country 
from movies 
wherer year_released = 2000
```
it may return duplicate results. So ...
```SQL
select distinct country 
from movies 
wherer year_released = 2000
```
```SQL
select distinct country, year_released -- The selected combination (country, year_released) will be identical.
from movies where year_released in (2000, 2001)
```
## Aggregate functions
```SQL
select country
