# Football Matches - Tasks

postgreSQL Queries on football_data.sql dataset.


## MVP:

1) Find all the matches from 2017.

```sql
SELECT * FROM matches WHERE season = 2017;
```

2) Find all the matches featuring Barcelona.

```sql
SELECT 
    * 
FROM matches WHERE hometeam = 'Barcelona' OR awayteam = 'Barcelona';
```

3) What are the names of the Scottish divisions included?

```sql
SELECT 
    * 
FROM divisions 
WHERE country = 'Scotland';
```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql
SELECT 
	COUNT(*) 
FROM matches 
WHERE 
	division_code = (SELECT code FROM divisions WHERE name = 'Bundesliga') AND
	(hometeam = 'Freiburg' OR awayteam = 'Freiburg');
```

5)  Find the teams which include the word "City" in their name. HINT: Not every team has been entered into the database with their full name, eg. `Norwich City` are listed as `Norwich`. If your query is correct it should return four teams.

```sql
SELECT 
	awayteam
FROM matches 
WHERE 
	LOWER(awayteam) LIKE '%city%'
GROUP BY awayteam;
```

6) How many different teams have played in matches recorded in a French division?

```sql
SELECT
	COUNT(DISTINCT hometeam)
FROM
	matches
WHERE
	division_code IN
	(SELECT 
		code
	FROM
		divisions
	WHERE
		country = 'France')
;
```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
SELECT 
	COUNT(*)
FROM
	matches
WHERE
	LOWER(hometeam) LIKE '%swansea%' AND
	LOWER(awayteam) LIKE '%huddersfield%'
;
```


## Extensions

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
<!-- Copy solution here -->


```

9) Select the matches played in the Premier League in order of total goals scored (`fthg` + `ftag`) from highest to lowest. When two matches have the same total the match with more home goals (`fthg`) should come first. 

```sql
<!-- Copy solution here -->


```

10) Find the name of the division in which the most goals were scored in a single season and the year in which it happened.

```sql
<!-- Copy solution here -->


```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)