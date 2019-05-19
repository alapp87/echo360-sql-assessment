# Echo360 SQL Assessment

# SQL problems

## Question 1

Given the following table:

track_media

|auto_inc | mediaid | modified |
| ------- | ------- | -------- |
|1        |	x       |2001-02-01|
|2        |	x       |2001-01-31|
|3        |	y       |2001-01-31|
|4        |	y       |2001-02-01|
|5        |	y       |2001-01-30|
|6        |	z       |2001-01-26|


Write a SQL query that yields the most recently modified auto_inc value for each mediaid.

```sql
SELECT auto_inc
FROM track_media t1
WHERE modified = (
	SELECT MAX(modified)
	FROM track_media t2
	WHERE t1.mediaid = t2.mediaid
);
```

Returns the below results:

|auto_inc|
| ------ |
|1       |
|4       |
|6       |


## Question 2

Given the tables:

user_sales		

|userid	| saleid |
| ----- | ------ |
|1|	1|	
|1|	2|	
|1|	3|	
|2|	3|	
|2|	4|	
|3|	5|	
|3|	6|	
|3|	7|	
|4|	8|	
		
sale_amount		

|saleid	| amount |	
| ----- | ------ |
|1	|$4.00 	 |
|2	|$3.50 	 |
|3	|$2.00 	 |
|4	|$3.75   |
|5	|$5.25 	 |
|6	|$3.00 	 |
		
Write a SQL query that yields the userids that have total sale amounts greater than 4 dollars and less than 6 dollars.

```sql
SELECT userid FROM (
	SELECT u1.userid AS userid, SUM(s1.amount) AS total_amount
	FROM user_sales u1
	JOIN sale_amount s1
	ON u1.saleid = s1.saleid
	GROUP BY u1.userid
	HAVING total_amount > 4
	AND total_amount < 6
);
```

Returns the below results:

|userid|
| ---- |
|2     |


