---
title: Data Analyst in SQL
tags:
  - SQL
  - database
  - tutorial
  - "#postgresql"
  - "#pgadmin"
  - "#sqlite3"
  - "#SQLiteStudio"
created: 2025-04-27
updated: 2025-05-10
author: Tonmoy
status: in-progress
resource:
---
# Data Communication Concepts
<a id="data-communication-concepts"></a>
* Fundamentals of Storytelling
<a id="fundamentals-of-storytelling"></a>
```sql
--Translating technical results
--Impacting decision-making process
--Not about spinning results!
--Making results stick:
	--Simple
	--Concrete
	--Credible

--Data storytelling road
	-- Story -> Tech or Not Tech -> Data -> Viz -> Present

-- Why are stories needed?
	--The best results have no impact without proper presentation
	--Convince change-adverse stakeholders
	--Non-technical stakeholders

--What is data storytelling?
	/*Data storytelling is the practice of building a narrative around a set of data and its
	accompanying visualizations to help convey the meaning of that data in a powerful and
	compelling fashion 
	*/
	--Anecdotes = imagination
	--Stories = memorable
	--Add value (provide context)
	--Capture audience's attention
	--Facilitate decision-making
	--Drive change

--Data storytelling
	--3-minutes story:
		--What would you say in 3 minutes?
	--Big idea:
		--Unique point of view
	--One sentence
		-- Clear and concise
--Data storytelling
	--1. Insightful
	--2. Explanatory
	--3. Concise
--Data
	--Results (e.g predictions) and findings (e.g. data analysis)
	--Relevant
	--Accurate and reliable
	--Actionable insights
--Narrative
	--Compelling and easy to understand
	--Prioritize essential points
	--Drive change
	--Main point:
		--Avoid disconnected facts
		--Central insight
	--Explanatory context:
		--Understand background and audience
		--Clarify facts to that audience
	--Linear sequence
--Visuals
	--Graphs should be:
		--simple
		--engaging
		--not misleading
```
---
* Translating Technical Results
<a id="translating-technical-results"></a>
```sql
--Data storytelling
	--Benefits:
		--Helps focus attention
		--Meaning and context
		--Helps retain insights
		--Better-informed decision-making
		--Persuade change-resistant stakeholders
--Tech or non-tech approach?
	--Technical knowledge is a continuum
	--Data professionals care about their methods...
	--...but the audience likely cares more about results and implications
--How technical?
	--Low accuracy predictions to supply chain agents
		--Don't care about stats
		--Care about their own pain points
--Translating technical results into stories
	--Easy to understand
	--Engage audience
	--Decision-making
	--Drive change
	--Strategies

--Awareness
	--What do they know?         --Adjust content
	--How our model works        	--Prediction's impact and limitations
	--What do they need to understand?     	--Be conversational
	--Why we chose our predictive variables   --The context on which our model works
	--What level of information do they need?  	--Serve audience
	--The correlation coefficients between variables 	--The interactions between customer traits
	

--ADEPT
	--Analogy
	--Diagram
	--Example
	--Plain English
	--Technical definition

--Technical jargon
	--Use acronyms with caution
		--Can help or hurt communication
		--Introduce the term and acronym
	--Jargon
		--Translate terminology
		--Simple terms
		--Guide
		--Definitions

--Focus on impact
	--Instead of
		--Use a non-relational database to make efficient nested queries.
		--Number of rooms shows correlation of 0.7 with a house price.
	--Focus on
		--Changing the storage approach will save a lot of time.
		--The more rooms in the house, the higher the price.

--Humility
	--Be receptive
	--Proactively ensure understanding
	--Explain differently
```
---
* Impacting the Decision making Process
<a id="impacting-the-decision-making-process"></a>
```sql
--Data storytelling
	--1. Data
	--2. Narrative
	--3. Visuals

--Compelling narrative
	--Meaningful to target audience
	--Prioritize key points
	--Drive change
/*
A description of connected events that organizes information to engage the audience and make them care for the results or information shared
*/

--Narrative structure:
	--->Background
	--What motivated the analysis?
	--What changed?
	--Who is the focus of the analysis?
		--Customers? Employees? Something else?
	--Our background: Total profit decreased

--Narrative structure
	-- ->Background -> Insight 1
	--What contributed to the problem?
	--Only relevant information
	--Our insight: Chips 20% increase. Sweets 30% decrease.

--Narrative structure
	-- ->Background -> Insight 1 -> Insight 2
	--Add supporting evidence
	--Help better explain the cause of problem
	--More insights: Most popular chocolate 50% decreased.

--Narrative structure
	-- ->Background -> Insight 1 -> Insight 2 -> Climax
	--Central insight
	--What would happen if there is no change
	--Our climax: Loss $10M next year.

--Narrative structure
	-- ->Background -> Insight 1 -> Insight 2 -> Climax -> Next Steps
	--Potential solutions
	--Course of action
	--Proactive
	--Our next steps: Rebrand chocolate.

--Building narrative
	--Change over time: Chocolate lower in summer and higher in winter.
	--Correlation: Chocolate rating vs. price
	--Comparison: Two age groups vs. chocolate consumption
	--Clustering: Groups with different coffee and chocolate consumption
```
---
# Data Driven Decision Making in SQL
<a id="data-driven-decision-making-in-sql"></a>
* Creating Database on PgAdmin and Importing Dataset
<a id="creating-database-on-pgadmin-and-importing-dataset"></a>
```sql
CREATE DATABASE movienow;
-> Right-click Databases -> Refresh ->Right-click movienow -> Select Query Tool
-> paste below sql query to import all dataset

DROP TABLE IF EXISTS "movies";
CREATE TABLE movies
(
    movie_id INT PRIMARY KEY,
    title TEXT,
    genre TEXT,
    runtime INT,
    year_of_release INT,
    renting_price numeric
);


COPY movies
	FROM PROGRAM 'curl "https://assets.datacamp.com/production/repositories/4068/datasets/3eebf2a145b76fee37357bcd55ac54577c03c805/movies_181127_2.csv"' (DELIMITER ',', FORMAT CSV, HEADER);


DROP TABLE IF EXISTS "actors";
CREATE TABLE actors
(
    actor_id integer PRIMARY KEY,
    name character varying,
    year_of_birth integer,
    nationality character varying,
    gender character varying
);


COPY actors
	FROM PROGRAM 'curl "https://assets.datacamp.com/production/repositories/4068/datasets/c67f20fa317e8229eed7586cda8bfce5fc177444/actors_181127_2.csv"' (DELIMITER ',', FORMAT CSV, HEADER);


DROP TABLE IF EXISTS "actsin";
CREATE TABLE actsin
(
    actsin_id integer PRIMARY KEY,
    movie_id integer,
    actor_id integer
);


COPY actsin
	FROM PROGRAM 'curl "https://assets.datacamp.com/production/repositories/4068/datasets/6efc08575effcc9327c82fea18aaf22dfd61cc27/actsin_181127_2.csv"' (DELIMITER ',', FORMAT CSV, HEADER);


DROP TABLE IF EXISTS "customers";
CREATE TABLE customers
(
	customer_id integer PRIMARY KEY,
    name character varying,
    country character varying,
    gender character varying,
    date_of_birth date,
    date_account_start date
);


COPY customers
	FROM PROGRAM 'curl "https://assets.datacamp.com/production/repositories/4068/datasets/4b1767d8e638ab26e62d98517fef297d72260992/customers_181127_2.csv"' (DELIMITER ',', FORMAT CSV, HEADER);


DROP TABLE IF EXISTS "renting";
CREATE TABLE renting
(
    renting_id integer PRIMARY KEY,
    customer_id integer NOT NULL,
    movie_id integer NOT NULL,
    rating integer,
    date_renting date
);


COPY renting
	FROM PROGRAM 'curl "https://assets.datacamp.com/production/repositories/4068/datasets/d36ed7719976092a9b3387c8a2ac077914c9e1d2/renting_181127_2.csv"' (DELIMITER ',', FORMAT CSV, HEADER);
```
---
* Introduction to Business Intelligence For A Online Movie Rental Database
<a id="introduction-to-business-intelligence-for-online-movie-rental-database"></a>
```sql
				--- Filtering and Ordering ---
select * 
from customers
where country = 'Italy';
-- Operators in WHERE clauese: =,<>,<,>,<=,>=,BETWEEN,IN,IS NULL, IS NOT NULL
select *
from movies
where genre <> 'Drama';

select *
from  movies
where renting_price >= 2;

select *
from customers
where date_account_start BETWEEN '2018-01-01' and '2018-09-30';

select * 
from actors
where nationality in ('USA', 'Australia');

select *
from renting
where rating IS NULL;

select *
from renting
where rating IS NOT NULL;

select name, date_account_start
from customers
where country = 'Italy'
AND date_account_start BETWEEN '2018-01-01' and '2018-09-30';

select name, country, date_account_start
from customers
where country = 'Italy'
OR date_account_start BETWEEN '2018-01-01' and '2018-09-30';

select * 
from renting
where rating is not null
order by rating ;

select * 
from renting
where rating is not null
order by rating desc;

				--Aggregations -summarizing data --
select AVG(renting_price)
from movies;
-- Some aggregate functions in SQL: AVG(),SUM(),COUNT(),MIN(),MAX()
select count(*)
from actors;

select count(name)
from actors;

select count(year_of_birth)
from actors;

select distinct country
from customers;

select count(distinct country)
from customers;

select distinct rating
from renting
order by rating;

select 
	AVG(renting_price) as average_price,
	count(distinct genre) as number_genres
from movies;
```
---
* Decision Making With Simple SQL Queries
<a id="decision-making-with-simple-sql-queries"></a>
```sql
				-- Grouping Movies --
CREATE TABLE movies_selected (
    title VARCHAR(100) NOT NULL,
    genre VARCHAR(50) NOT NULL,
    renting_price DECIMAL(4,2) NOT NULL
);

INSERT INTO movies_selected (title, genre, renting_price) VALUES
('Fight Club', 'Drama', 2.49),
('The Lord of the Rings: The Fellowship of the Ring', 'Fantasy', 2.59),
('The Lord of the Rings: The Two Towers', 'Fantasy', 2.69),
('The Lord of the Rings: The Return of the King', 'Fantasy', 2.79),
('The Prestige', 'Sci-Fiction', 2.85),
('Ratatouille', 'Animation', 2.89),
('WALL.E', 'Animation', 2.89),
('Inception', 'Sci-Fiction', 2.89),
('The Big Shot', 'Drama', 2.99),
('The Imitation Game', 'Drama', 2.99),
('Moonlight', 'Drama', 2.99),
('LaLaLand', 'Romance', 2.99),
('Zootopia', 'Animation', 2.99);

select genre
from movies_selected
group by genre;

select genre, avg(renting_price) as avg_price
from movies_selected
group by genre;

select 
	genre, round(avg(renting_price),2) as avg_price, count(*) as number_movies
from movies_selected
group by genre;

select 
	genre, round(avg(renting_price),2) as avg_price, count(*) as number_movies
from movies_selected
group by genre
having count(*)>2;

			--joining movie ratings with customer data--
select * 
from customers as c
where c.customer_id =2;

select * 
from renting as r
left join customers as c
on r.customer_id = c.customer_id;

select m.title,c.name
from renting as r
left join movies as m
on r.movie_id =m.movie_id
left join customers as c
on r.customer_id = c.customer_id;

			-- Money spent per customer with subqueries--
select *
from actors
where gender = 'female';

select
	af.nationality,
	Min(af.year_of_birth),
	Max(af.year_of_birth)
from
(
	select *
	from actors
	where gender = 'female'
)as af
group by af.nationality;

select 
	r.customer_id,
	m.renting_price
from renting as r
left join movies as m
on r.movie_id = m.movie_id
order by r.customer_id;

select 
	rm.customer_id,
	sum(rm.renting_price)
from(
	select 
		r.customer_id,
		m.renting_price
	from renting as r
	left join movies as m
	on r.movie_id = m.movie_id	
) as rm
group by rm.customer_id;

			-- Identify favourite actors of customer groups--
select *
from renting as r
left join customers as c
on c.customer_id = r.customer_id
left join actsin as ai
on r.movie_id = ai.movie_id
left join actors as a
on a.actor_id = ai.actor_id;

select 
	a.name as actor_name, 
	count(*) as renting_times,
	round(avg(r.rating),2)as avg_rating
from renting as r
left join customers as c
on c.customer_id = r.customer_id
left join actsin as ai
on r.movie_id = ai.movie_id
left join actors as a
on a.actor_id = ai.actor_id
where c.gender = 'male' -- male customers 
group by a.name
having avg(r.rating) is not null
order by avg_rating desc, renting_times desc;

```
---
* Data Driven Decision Making With Advanced SQL Queries
<a id="data-driven-decision-making-with-advanced-sql-queries"></a>
```sql
			-- Nested queries--
select name
from customers
where customer_id in
(
	select distinct customer_id
	from renting
	where rating <=3
);

select country , min(date_account_start)
from customers
group by country
having min(date_account_start) <
(
	select min(date_account_start)
	from customers
	where country ='Austria'
);

select name
from actors
where actor_id in
(
	select actor_id
	from actsin
	where movie_id =
	(
		select movie_id
		from movies
		where title ='Ray'
	)
);

			-- Correlated nested queries--
			
-- Number of movie rentals more than 5
select * 
from movies as m
where 5 <
(
	select count(*)
	from renting as r
	where r.movie_id = m.movie_id
);

-- Number of movie rentals less than 5
select * 
from movies as m
where 5 >
(
	select count(*)
	from renting as r
	where r.movie_id = m.movie_id
);

			-- Queries with EXISTS --

-- Movies with at least one rating
select *
from movies as m
where exists
(
	select * 
	from renting as r
	where rating is not null
	and r.movie_id = m.movie_id
);

-- Movies with no rating
select *
from movies as m
where not exists
(
	select * 
	from renting as r
	where rating is not null
	and r.movie_id = m.movie_id
);

			-- Queries with UNION an INTERSECT --
select 
	title, genre, renting_price
from movies
where renting_price > 2.8
UNION -- giving no duplicates
select
	title, genre, renting_price
from movies
where genre = 'Action & Adventure';

select 
	title, genre, renting_price
from movies
where renting_price > 2.8
INTERSECT
select
	title, genre, renting_price
from movies
where genre = 'Action & Adventure';

select 
	title, genre, renting_price
from movies
where renting_price > 2.8
union all -- giving duplicates
select
	title, genre, renting_price
from movies
where genre = 'Action & Adventure';

```
--- 
* Data Driven Decision Making With Olap SQL Queries
<a id="data-driven-decision-making-with-olap-sql-queries"></a>
```sql
			-- OLAP:(online analytical processing) CUBE operator--
select 
	country, genre,count(*) as rental_count
from
(
	select 
		r.renting_id,c.country,m.genre, r.rating
	from renting as r
	left join customers as c
	on r.customer_id = c.customer_id
	left join movies as m
	on r.movie_id = m.movie_id
	where c.country in ('Austria', 'Belgium')
	and m.genre in('Drama', 'Comedy')
) as subquery
group by cube(country,genre)
order by 
	case
		when country is not null and  genre is not null  then 1
		when country is not null and genre is null then  3
		end
	;

--Number of ratings
select 
	country, genre,count(rating) as rating_count
from
(
	select 
		r.renting_id,c.country,m.genre, r.rating
	from renting as r
	left join customers as c
	on r.customer_id = c.customer_id
	left join movies as m
	on r.movie_id = m.movie_id
	where c.country in ('Austria', 'Belgium')
	and m.genre in('Drama', 'Comedy')
) as subquery
group by cube(country,genre)
order by 
	case
		when country is not null and  genre is not null  then 1
		when country is not null and genre is null then  3
		end
	;

			--Queries with ROLLUP --
select 
	country, genre,count(*) as rental_count
from
(
	select 
		r.renting_id,c.country,m.genre, r.rating
	from renting as r
	left join customers as c
	on r.customer_id = c.customer_id
	left join movies as m
	on r.movie_id = m.movie_id
	where c.country in ('Austria', 'Belgium')
	and m.genre in('Drama', 'Comedy')
) as subquery
group by rollup(country,genre) -- all combination with country
order by 
	case
		when country is not null and  genre is not null  then 1
		when country is not null and genre is null then  3
		end
	;

select 
	country, genre,count(*) as rental_count
from
(
	select 
		r.renting_id,c.country,m.genre, r.rating
	from renting as r
	left join customers as c
	on r.customer_id = c.customer_id
	left join movies as m
	on r.movie_id = m.movie_id
	where c.country in ('Austria', 'Belgium')
	and m.genre in('Drama', 'Comedy')
) as subquery
group by rollup(genre, country) -- all combination with genre
order by 
	case
		when country is not null and  genre is not null  then 1
		when country is not null and genre is null then  3
		end
	;

select 
	country, genre,
	count(*) as rental_count, count(rating) as rating_count
from
(
	select 
		r.renting_id,c.country,m.genre, r.rating
	from renting as r
	left join customers as c
	on r.customer_id = c.customer_id
	left join movies as m
	on r.movie_id = m.movie_id
	where c.country in ('Austria', 'Belgium')
	and m.genre in('Drama', 'Comedy')
) as subquery
group by rollup(country,genre) -- all combination with country
order by 
	case
		when country is not null and  genre is not null  then 1
		when country is not null and genre is null then  3
		end
	;

			-- Group by GROUPING SETS--

create view renting_extended as
select 
	r.renting_id,c.country,m.genre, r.rating
from renting as r
left join customers as c
on r.customer_id = c.customer_id
left join movies as m
on r.movie_id = m.movie_id
where c.country in ('Austria', 'Belgium')
and m.genre in('Drama', 'Comedy');

			
--same as group by cube (country, genre)
SELECT 
	country, genre, count(*)
from renting_extended
group by GROUPING SETS((country,genre),(country), (genre), ()) 
order by 
	case
		when country is not null and  genre is not null  then 1
		when country is not null and genre is null then  3
		end
	;
--Explanation: UNION of all these queries become above query--
select country, genre, count(*)
from renting_extended
group by grouping sets ((country, genre));
--group by grouping sets (country, genre); -- not same
--same as

select country, genre, count(*)
from renting_extended
group by country, genre;

select country, count(*)
from renting_extended
group by grouping sets (country);
--same as
select country, count(*)
from renting_extended
group by country;

select genre, count(*)
from renting_extended
group by grouping sets (genre);
--same as
select genre, count(*)
from renting_extended
group by genre;

select count(*)
from renting_extended
group by grouping sets (());
--same as
select count(*)
from renting_extended;
--------------------
--calculate number of rentals and avg_rating group by (country, genre) & only genre
select country, genre, count(*), ROUND(avg(rating),2) as avg_rating
from renting_extended
group by grouping sets((country, genre), (genre));

			-- Final example--
-- movies with at least 4 person ratings & rentals since 2018-04-01
-- i don't understand why 2002 and 2004 has 2 rows one with null ratings
select 
	m.year_of_release,
	c.country,
	count(*) as n_rentals,
	count(distinct r.movie_id) as n_movies,
	ROUND(avg(rating),2) as avg_rating
from renting as r
left join customers as c
on r.customer_id = c.customer_id
left join movies as m
	on r.movie_id = m.movie_id
where r.movie_id in
(
	select movie_id 
	from renting
	group by movie_id
	having count(rating) >=4
)
and r.date_renting >= '2018-04-01'
group by ROLLUP	(m.year_of_release, c.country)
order by c.country, m.year_of_release;

```
---
# Data Manipulation in SQL
<a id="data-manipulation-in-sql"></a>
* Prerequisite :
<a id="prerequisite"></a>
```sql
/*
	download # SQLiteStudio: 
		https://sqlitestudio.pl/  -> download 
		chmod +x SQLiteStudio-3.4.17-linux-x64-installer.run
		./SQLiteStudio-3.4.17-linux-x64-installer.run
	
	Install sqlite3:
		sudo apt update
		sudo apt install sqlite3
		sqlite3 --version

	Import data set:
		open SQLiteStudio
		select -> 'add a database from dashboard'
		select -> browse for existing database file from loccal computer
			which is database.sqlite
		select ->  ok
	Run queries:
		click Tools -> Open SQL editor
	Done
	

*/
```
---
* Well Take The Case
<a id="well-take-the-case"></a>
```sql
           --- welcome to intermediate sql--
select
    l.name as league,
    count(m.country_id) as total_match
from league as l
left join match as m
on l.country_id = m.country_id
group by l.name;

select * from match 
where date = '2008-08-17 00:00:00'
limit 10;

select 
    [date], id, home_team_goal, away_team_goal
from match
where season = '2013/2014'

select 
    [date], id, home_team_goal, away_team_goal,
    case
        when home_team_goal > away_team_goal then ' Home team win '
        when home_team_goal < away_team_goal then ' Away team win '
        else 'Tie'
    end as outcome
from match
where season = '2013/2014';

            --IN CASE things get more complex--
select date,
    case
        when date > '2015-01-01' then 'more recently'
        when date < '2012-01-01' then 'more older'
        end as date_category
from match; -- this create some null values between '2015-01-01' and '2015-01-01'

select date,
    case
        when date > '2015-01-01' then 'more recently'
        when date < '2012-01-01' then 'more older'
        else null
        end as date_category
from match; -- this create some null values between '2015-01-01' and '2015-01-01'

select * from match 
where home_team_api_id = 8455
limit 10;

select 
    [date], home_team_api_id, away_team_api_id,
    case
        when home_team_api_id = 8455 and home_team_goal > away_team_goal
        then 'Chelsea home win'
        when home_team_api_id = 8455 and home_team_goal < away_team_goal
        then 'Chelsea away win'
        else 'Loss or tie'
        end as outcome
from match
where home_team_api_id = 8455 or away_team_api_id =8455;

select 
    [date], home_team_api_id, away_team_api_id,
    case
        when home_team_api_id = 8455 and home_team_goal > away_team_goal
        then 'Chelsea home win'
        when home_team_api_id = 8455 and home_team_goal < away_team_goal
        then 'Chelsea away win'
        end as outcome
from match-- this will show some null values
where home_team_api_id = 8455 or away_team_api_id =8455;

select 
    [date], home_team_api_id, away_team_api_id,
    case
        when home_team_api_id = 8455 and home_team_goal > away_team_goal
        then 'Chelsea home win'
        when home_team_api_id = 8455 and home_team_goal < away_team_goal
        then 'Chelsea away win'
        end as outcome
from match
where 
    case
        when home_team_api_id = 8455 and home_team_goal > away_team_goal
        then 'Chelsea home win'
        when home_team_api_id = 8455 and home_team_goal < away_team_goal
        then 'Chelsea away win'
        end is not null;-- filter with case and  exclude null values

            --case when with agggregate functions--
select
    season,
    count(case when home_team_api_id = 8650
                and home_team_goal > away_team_goal
                then id end) as home_wins,
    count(case when away_team_api_id = 8650
                and home_team_goal < away_team_goal
                then 'id or anything' end) as away_wins
from match
group by season;

select
    season,
    sum(case when home_team_api_id = 8650
                then home_team_goal end) as home_goals,
    sum(case when away_team_api_id = 8650
                then away_team_goal end) as away_gooals
from match
group by season;

select
    season,
    round(avg(case when home_team_api_id = 8650
                then home_team_goal end),2) as avg_home_goals,
    round(avg(case when away_team_api_id = 8650
                then away_team_goal end),2) as avg_away_gooals
from match
group by season;

-- Percentages with case and avg
select
    season,
    round(avg(case 
        when home_team_api_id = 8455 and home_team_goal > away_team_goal then 1
        when home_team_api_id = 8455 and home_team_goal < away_team_goal then 0
         end),2) as pct_home_wins,
     round(avg(case 
        when away_team_api_id = 8455 and home_team_goal < away_team_goal then 1
        when away_team_api_id = 8455 and home_team_goal > away_team_goal then 0
         end),2) as pct_away_wins
from match
group by season;

```
---
* Short And Simple Subqueries
<a id="short-and-simple-subqueries"></a>
```sql
            -- where are the subqueries--
select home_team_goal
from match
where home_team_goal >(
    select avg(home_team_goal) from match);

-- team home goals higher than average home goals    
select 
    date, home_team_api_id, away_team_api_id, 
    home_team_goal, away_team_goal
from match
where season = '2012/2013'
and home_team_goal > (select avg(home_team_goal) from match);

-- team that are part of poland's league
select 
    team_long_name, team_short_name as abbr
from team
where
    team_api_id in(
                select home_team_api_id
                from match
                where country_id =15722
                    );
            
            -- subqueries in the from statement--
-- 3 teams has the highest average of home goals
select team_name, home_avg_goal
from
(
    select
        t.team_long_name as team_name,
        avg(m.home_team_goal) home_avg_goal
    from match as m
    left join team as t
    on m.home_team_api_id = t.team_api_id
    where season = '2011/2012'
    group by team_name
) as subquery
order by 2 desc limit 3;

            --Subqueries in select--
select count(id) from match;

select 
    season,
    count(id) as matches,
    (select count(id) from match) as total_matches
from match
group by season; 

-- average goals in perticular season

select avg(home_team_goal + away_team_goal)
from match
where season = '2011/2012'

select 
    date,
    (home_team_goal + away_team_goal) as per_match_goals,
    (home_team_goal + away_team_goal)-
        (select 
            avg(home_team_goal + away_team_goal)
        from match
        where season = '2011/2012') as diff_from_avg_goals
        -- here where is must needed otherwise all season avg will be calculated
from match
where season = '2011/2012';

            -- subqueries everywhere and best practices--
-- not good practice
elect
    matches.country_id,
    round(avg(matches.home_team_goal + matches.away_team_goal),2) as avg_goals,
    (select round(avg(home_team_goal + away_team_goal),2)
        from match 
        where season = '2013/2014') as overall_avg
from (
    select
        id,country_id, home_team_goal, away_team_goal, season
    from match
    where home_team_goal > 5
    ) as matches
where 
    matches.season = '2013/2014'
   /* and
        (avg(matches.home_team_goal + matches.away_team_goal)>
            (select round(avg(home_team_goal + away_team_goal),2)
        from match 
        where season = '2013/2014')
        )*/-- Error while executing SQL query on database 'database': misuse of aggregate: avg()
group by matches.country_id

-- Best Practices with CTE
WITH overall_stats AS (
    SELECT round(avg(home_team_goal + away_team_goal), 2) as overall_avg
    FROM match
    WHERE season = '2013/2014'
),
country_stats AS (
    SELECT 
        country_id,
        round(avg(home_team_goal + away_team_goal), 2) as avg_goals
    FROM match
    WHERE 
        season = '2013/2014'
        AND home_team_goal > 5
    GROUP BY country_id
)
SELECT 
    cs.country_id,
    cs.avg_goals,
    os.overall_avg
FROM country_stats cs
CROSS JOIN overall_stats os
WHERE cs.avg_goals > os.overall_avg;

```
---
* Correlated Queries Nested Queries And Common Table Expressions
<a id="correlated-queries-nested-queries-and-common-table-expressions"></a>
```sql
           -- correlated subqueries--
select 
    s.stage,
    round(s.avg_goals,2) as avg_goal,
    (select avg(home_team_goal + away_team_goal)
        from match
        where season = '2012/2013') as overall_avg
from
(
    select 
        stage,
        avg(home_team_goal+ away_team_goal) as avg_goals
    from match
    where season = '2012/2013' 
    group by stage
) as s
where
    s.avg_goals > (select avg(home_team_goal + away_team_goal) 
        from match
        where season = '2012/2013')

-- with CTE
with overall_stat as(
    select avg(home_team_goal + away_team_goal) as overall_avg
        from match
        where season = '2012/2013'
),
stat as(
    select 
        stage,
        avg(home_team_goal+ away_team_goal) as avg_goals
    from match
    where season = '2012/2013' 
    group by stage
)
select
    s.stage,
    round(s.avg_goals,2) as avg_goal,
    os.overall_avg
from stat as s
cross join overall_stat as os
where s.avg_goals > os.overall_avg

-- A correlated example
select 
    s.stage,
    round(s.avg_goals,2) as avg_goal,
    (select avg(home_team_goal + away_team_goal)
        from match
        where season = '2012/2013') as overall_avg
from
(
    select 
        stage,
        avg(home_team_goal+ away_team_goal) as avg_goals
    from match
    where season = '2012/2013' 
    group by stage
) as s
where
    s.avg_goals > 
	    (select avg(home_team_goal + away_team_goal) 
        from match as m
        where s.stage > m.stage);
			        --filters stages where the average goals are higher than 
                    --the average of previous stages. like when s.stage =4 then it compare avg(m.stage 1,2,3)

--average number of goals score by each country
select 
    c.name as country_name,
    avg(m.home_team_goal + m.away_team_goal) as avg_goals
from country as c
left join match as m
on c.id = m.country_id
group by country_name;

-- same output but using correlated subqueries
select 
    c.name as country_name,
    (select 
        avg(m.home_team_goal + m.away_team_goal) 
     from match as m
     where c.id = m.country_id
    )as avg_goals
from country as c;

            --Nested subqueries--
            
-- each country's average differ from the overall average
select 
    c.name as country_name,
    avg(m.home_team_goal + m.away_team_goal) as avg_goals,
    avg(m.home_team_goal + m.away_team_goal) -
        (select avg(home_team_goal + away_team_goal)
        from match) as avg_diff
from country as c
left join match as m
on c.id = m.country_id
group by country_name;

-- each month's total goal differ form the average monthly total of goals
select
    strftime('%m', date) as month,
    sum(m.home_team_goal + m.away_team_goal) as total_goals,
    sum(m.home_team_goal + m.away_team_goal)-
        (select avg(goals)
            from(select
                    strftime('%m', date) as month,
                    sum(home_team_goal + away_team_goal) as goals
                    from match
                    group by month)) as avg_diff
from match as m
group by month;
                
-- each country average goal in '2011/2012' seson
select 
    c.name as country_name,
     (select avg(m.home_team_goal + m.away_team_goal)
        from match as m
        where m.country_id = c.id --correlate with main query
        and id in(
            select id from match 
            where season ='2011/2012')) as avg_goals
from country as c
--group by country_name;
    
            -- common table expression or CTE--
-- without CTE
select 
    c.name as country_name,
    count(s.id) as matches
from country as c
inner join (select
                country_id, id
                from match
                where (home_team_goal + away_team_goal)>= 10
            ) as s
on c.id = s.country_id
group by country_name;

-- With CTEs
with goal_GT10 as (
        select
            country_id, id
        from match
        where (home_team_goal + away_team_goal)>= 10
        )
select 
        c.name as country_name,
        count(g.id) as matches
from country as c
inner join goal_GT10 as g
on g.country_id = c.id
group by country_name

with s1 as (
        select
            country_id, id
        from match
        where (home_team_goal + away_team_goal)>= 10
        ),
 s2 as (
        select
            country_id, id
        from match
        where (home_team_goal + away_team_goal)<= 1
        )
select
    c.id as CountryID,
    c.name as country_name,
    count(distinct s1.id) as high_scores, 
    count(distinct s2.id) as low_scores
    /*sicne high score matches < low score matches 
    so, duplicate row join s1.id occure so make sure use distinct*/
from country as c
inner join s1
on s1.country_id = c.id
inner join s2
on s2.country_id = c.id
group by country_name;
/*
select
    c.id as CountryID,
    c.name as country_name,s1.id,s2.id
from country as c
left join s1
on s1.country_id = c.id
left join s2
on s2.country_id = c.id
where c.id = 7809
*/

```
---
* Window Functions
<a id="window-functions"></a>
```sql
            --Window function--
-- Without window function
with stat as(
    select avg(home_team_goal + away_team_goal) as overall_avg
    from match
    where season ='2011/2012')
select 
    date, 
    (home_team_goal + away_team_goal) total_goals,
    (select * from stat) as overall_avg
    --stat.overall_avg -- Works in some DBMS but not all
from match
--CROSS JOIN stat  -- or other JOIN types to use CTE
where season = '2011/2012';

-- With window function
-- goals were scored in each match compare to total_avg in season 2011/2012
select
    date,
    (home_team_goal + away_team_goal) as total_goals,
    avg(home_team_goal + away_team_goal) over() as overall_avg
from match
where season ='2011/2012';

--rank of matches based on number of goals
select 
    date,
    (home_team_goal + away_team_goal) as goals,
    rank() over(order by home_team_goal + away_team_goal desc) as top_goal_rank_not_perfect,
    rank() over(order by home_team_goal + away_team_goal desc,date) as top_goal_rank_perfect, 
    rank() over(partition by home_team_goal + away_team_goal order by home_team_goal + away_team_goal desc,date ) as rank_by_partition_of_goals,
    rank() over(partition by home_team_goal + away_team_goal order by home_team_goal + away_team_goal desc,date desc) as rank_by_partition_of_goals
from match
where season = '2011/2012'

                -- Window partitions--
-- goal score in each match compare this with seasonal average
select 
    date,
    goals, 
    season_avg,
    row_num
    
from
    (select
       date,
        (home_team_goal + away_team_goal) as goals,
        avg(home_team_goal + away_team_goal) over(partition by season) as season_avg,
        ROW_NUMBER() OVER(PARTITION BY date ORDER BY date) as row_num -- there is more than one match held in same date
    from match
)as sub
where 
    date in ('2008-12-12 00:00:00',
            '2009-12-12 00:00:00',
            '2010-12-12 00:00:00',
            '2011-12-12 00:00:00',
            '2012-12-12 00:00:00',
            '2014-12-12 00:00:00')
and row_num = 1;

-- compare total goal in every match and average that partition with country name and season
select
    c.name,
    m.season,
    (home_team_goal + away_team_goal) as goals,
    avg(home_team_goal + away_team_goal)
        over(partition by m.season,c.name) as season_ctry_avg
from country as c
left join match as m
on c.id = m.country_id

                -- sliding window--
-- syntax rows between <start> and <finish>
-- some keywords PRECEDING, FOLLOWING, 
--UNBOUNDED PRECEDING, UNBOUNDED FOLLOWING, CURRENT ROW

-- Manchester city home games
select 
    date,
    home_team_goal, away_team_goal,
    sum(home_team_goal)
        over(order by date rows between
                UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total,-- simple running total
    sum(home_team_goal)
        over(order by date rows between
                1 PRECEDING AND CURRENT ROW) AS running_totalP1, -- running total with any sum of current value and its previous value
    sum(home_team_goal)
        over(order by date rows between
                2 PRECEDING AND CURRENT ROW) AS running_totalP2  -- if 2 previous value not found its take that as 0 and  sum with current row
from match
where home_team_api_id = 8456 
and season = '2011/2012';

-- Manchester United or MNU defeted by those team in season 2013/2014
with MNU_loss_data as
(
    select 
        date,season,home_team_api_id,
        home_team_goal, 
        away_team_api_id,
        away_team_goal
        ,
        case
            when season = '2013/2014' and home_team_api_id = 10260 and home_team_goal < away_team_goal then away_team_api_id
            when season = '2013/2014' and away_team_api_id = 10260 and home_team_goal > away_team_goal then home_team_api_id
            end as outcome
    from match
    where 
        /*(home_team_api_id = 10260 or away_team_api_id =10260)*/
            case
                when season = '2013/2014' and home_team_api_id = 10260 and home_team_goal < away_team_goal then 'need'
                when season = '2013/2014' and away_team_api_id = 10260 and home_team_goal > away_team_goal then 'need'
            end is not  null
)
select distinct m.team_api_id,m.team_long_name
from team as m
inner join   MNU_loss_data as l
on  m.team_api_id  = l.outcome ; 

-- More clean way
with loss_data as
(
    select 
        date, season, home_team_api_id,
        home_team_goal, 
        away_team_api_id,
        away_team_goal
    from match
    where 
        (season = '2013/2014' AND home_team_api_id = 10260 AND home_team_goal < away_team_goal) OR
        (season = '2013/2014' AND away_team_api_id = 10260 AND home_team_goal > away_team_goal)
)
select m.team_api_id, m.team_long_name
from team as m
where m.team_api_id IN (
    select 
        case
            when home_team_api_id = 10260 and home_team_goal < away_team_goal then away_team_api_id
            when away_team_api_id = 10260 and home_team_goal > away_team_goal then home_team_api_id
        end
    from loss_data
);

-- Same thing but different
with loss_data as
(
    select 
        date,season,home_team_api_id,
        home_team_goal, 
        away_team_api_id,
        away_team_goal
        /*,
        case
            when season = '2013/2014' and home_team_api_id = 10260 and home_team_goal < away_team_goal then 'need'
            when season = '2013/2014' and away_team_api_id = 10260 and home_team_goal > away_team_goal then 'need'
            end as outcome*/
    from match
    where 
        /*(home_team_api_id = 10260 or away_team_api_id =10260)*/
            case
                when season = '2013/2014' and home_team_api_id = 10260 and home_team_goal < away_team_goal then 'need'
                when season = '2013/2014' and away_team_api_id = 10260 and home_team_goal > away_team_goal then 'need'
            end is not  null
)
select m.team_api_id,m.team_long_name
from team as m
where m.team_api_id in(
    select
    case
            when home_team_api_id = 10260 and home_team_goal < away_team_goal then away_team_api_id
            when away_team_api_id = 10260 and home_team_goal > away_team_goal then home_team_api_id
            end

   from loss_data );
    
--Team that defets Manchester United with their goals and rank
with MNU_loss_data as
(
    select 
        date,season,home_team_api_id,
        home_team_goal, 
        away_team_api_id,
        away_team_goal
        ,
        case
            when season = '2013/2014' and home_team_api_id = 10260 and home_team_goal < away_team_goal then away_team_api_id
            when season = '2013/2014' and away_team_api_id = 10260 and home_team_goal > away_team_goal then home_team_api_id
            end as outcome,
        case
            when season = '2013/2014' and home_team_api_id = 10260 and home_team_goal < away_team_goal then away_team_goal
            when season = '2013/2014' and away_team_api_id = 10260 and home_team_goal > away_team_goal then home_team_goal
            end as goal_conceive
    from match
    where 
        /*(home_team_api_id = 10260 or away_team_api_id =10260)*/
            case
                when season = '2013/2014' and home_team_api_id = 10260 and home_team_goal < away_team_goal then 'need'
                when season = '2013/2014' and away_team_api_id = 10260 and home_team_goal > away_team_goal then 'need'
            end is not  null
)
select 
    m.team_api_id,m.team_long_name as MNU_defeted_by, l.goal_conceive as n_of_goals,
    rank() over(order by l.goal_conceive desc,m.team_long_name) as rank
from team as m
inner join   MNU_loss_data as l
on  m.team_api_id  = l.outcome;

```
---
# Exploratory Data Analysis in SQL
<a id="exploratory-data-analysis-in-sql"></a>
* Whats In The Database
<a id="whats-in-the-database"></a>
```sql
			-- Importing Dataset In PostgreSQL--
CREATE DATABASE eda2310;
-> Right-click Databases -> Refresh ->Right-click movienow -> Select Query Tool
-> paste below sql query to import all dataset


set time zone 'UTC';

drop table if exists evanston311;

create table evanston311 (
  id int primary key,
  priority varchar(6),
  source varchar(20),
  category varchar(64),
  date_created timestamp with time zone,
  date_completed timestamp with time zone,
  street varchar(48),
  house_num varchar(12),
  zip char(5),
  description text
);

COPY evanston311
	FROM PROGRAM 'curl "https://assets.datacamp.com/production/repositories/3567/datasets/48ea25f9557bdad445f18055f13903455189359c/ev311.csv"' (DELIMITER ',', FORMAT CSV, HEADER, NULL 'NA');


drop table if exists stackoverflow;
drop table if exists tag_type;
drop table if exists tag_company;
drop table if exists company;
drop table if exists fortune500;

create table company (
  id int primary key,
  exchange varchar(10),
  ticker char(5) unique,
  name varchar not null,
  parent_id int references company(id)
);
/*
1. `parent_id` as an integer that references the `id` column of the same table (a self-referential foreign key)
    
The self-referential foreign key (`parent_id` referencing `id`) allows you to create hierarchical relationships between companies, where a company can have a parent company that also exists in the same table.
*/

create table tag_company (
  tag varchar(30) primary key,
  company_id int references company(id)
);

create table stackoverflow (
   id serial,
   tag varchar(30) references tag_company(tag),
   date date,
   question_count integer default 0,  
   question_pct double precision, 
   unanswered_count integer,
   unanswered_pct double precision
);

create table tag_type (
  id serial,
  tag varchar(30) references tag_company(tag),
  type varchar(30)
);

create table fortune500 (
  rank int not null,
  title varchar primary key,
  name varchar not null unique,
  ticker char(5),
  url varchar,
  hq varchar,
  sector varchar,
  industry varchar,
  employees int check (employees > 0),
  revenues int,
  revenues_change real,
  profits numeric,
  profits_change real,
  assets numeric check (assets > 0),
  equity numeric
);

insert into company values 
(1, 'nasdaq', 'PYPL', 'PayPal Holdings Incorporated', NULL),
(2, 'nasdaq', 'AMZN', 'Amazon.com Inc', NULL),
(3, 'nasdaq', 'MSFT', 'Microsoft Corp.', NULL),
(4, 'nasdaq', 'MDB', 'MongoDB', NULL),
(5, 'nasdaq', 'DBX', 'Dropbox', NULL),
(6, 'nasdaq', 'AAPL', 'Apple Incorporated', NULL),
(7, 'nasdaq', 'CTXS', 'Citrix Systems', NULL),
(8, 'nasdaq', 'GOOGL', 'Alphabet', NULL),
(9, 'nyse', 'IBM', 'International Business Machines Corporation', NULL),
(10, 'nasdaq', 'ADBE', 'Adobe Systems Incorporated', NULL),
(11, NULL, NULL, 'Stripe', NULL),
(12, NULL, NULL, 'Amazon Web Services', 2),
(13, NULL, NULL, 'Google LLC', 8),
(14, 'nasdaq', 'EBAY', 'eBay, Inc.', NULL);


insert into tag_company (tag, company_id) values 
('actionscript', 10),
('actionscript-3', 10),
('amazon', 2),
('amazon-api', 2),
('amazon-appstore', 2),
('amazon-cloudformation', 12),
('amazon-cloudfront', 12),
('amazon-cloudsearch', 12),
('amazon-cloudwatch', 12),
('amazon-cognito', 12),
('amazon-data-pipeline', 12),
('amazon-dynamodb', 12),
('amazon-ebs', 12),
('amazon-ec2', 12),
('amazon-ecs', 12),
('amazon-elastic-beanstalk', 12),
('amazon-elasticache', 12),
('amazon-elb', 12),
('amazon-emr', 12),
('amazon-fire-tv', 2),
('amazon-glacier', 12),
('amazon-kinesis', 12),
('amazon-lambda', 12),
('amazon-mws', 12),
('amazon-rds', 12),
('amazon-rds-aurora', 12),
('amazon-redshift', 12),
('amazon-route53', 12),
('amazon-s3', 12),
('amazon-ses', 12),
('amazon-simpledb', 12),
('amazon-sns', 12),
('amazon-sqs', 12),
('amazon-swf', 12),
('amazon-vpc', 12),
('amazon-web-services', 12),
('android', 13),
('android-pay', 13),
('applepay', 6),
('applepayjs', 6),
('azure', 3),
('citrix', 7),
('cognos', 9),
('dropbox', 5),
('dropbox-api', 5),
('excel', 3),
('google-spreadsheet', 13),
('ios', 6),
('ios8', 6),
('ios9', 6),
('mongodb', 4),
('osx', 6),
('paypal', 1),
('sql-server', 3),
('stripe-payments', 11),
('windows', 3);

insert into tag_type (tag, type) values 
('amazon-cloudformation', 'cloud'),
('amazon-cloudfront', 'cloud'),
('amazon-cloudsearch', 'cloud'),
('amazon-cloudwatch', 'cloud'),
('amazon-cognito', 'cloud'),
('amazon-cognito', 'identity'),
('amazon-data-pipeline', 'cloud'),
('amazon-dynamodb', 'cloud'),
('amazon-dynamodb', 'database'),
('amazon-ebs', 'cloud'),
('amazon-ec2', 'cloud'),
('amazon-ecs', 'cloud'),
('amazon-elastic-beanstalk', 'cloud'),
('amazon-elasticache', 'cloud'),
('amazon-elb', 'cloud'),
('amazon-emr', 'cloud'),
('amazon-glacier', 'cloud'),
('amazon-glacier', 'storage'),
('amazon-kinesis', 'cloud'),
('amazon-lambda', 'cloud'),
('amazon-mws', 'api'),
('amazon-rds-aurora', 'cloud'),
('amazon-rds', 'cloud'),
('amazon-rds-aurora', 'database'),
('amazon-rds', 'database'),
('amazon-redshift', 'cloud'),
('amazon-route53', 'cloud'),
('amazon-s3', 'cloud'),
('amazon-ses', 'cloud'),
('amazon-simpledb', 'cloud'),
('amazon-simpledb', 'database'),
('amazon-sns', 'cloud'),
('amazon-sqs', 'cloud'),
('amazon-swf', 'cloud'),
('amazon-vpc', 'cloud'),
('amazon-web-services', 'cloud'),
('amazon', 'company'),
('android-pay', 'payment'),
('android', 'mobile-os'),
('applepay', 'payment'),
('applepayjs', 'payment'),
('azure', 'cloud'),
('citrix', 'company'),
('dropbox-api', 'api'),
('dropbox-api', 'api'),
('dropbox-api', 'api'),
('dropbox', 'storage'),
('dropbox', 'cloud'),
('dropbox', 'company'),
('excel', 'spreadsheet'),
('google-spreadsheet', 'spreadsheet'),
('ios', 'mobile-os'),
('ios8', 'mobile-os'),
('ios9', 'mobile-os'),
('mongodb', 'database'),
('osx', 'os'),
('paypal', 'payment'),
('paypal', 'company'),
('sql-server', 'database'),
('stripe-payments', 'payment'),
('windows', 'os');


COPY stackoverflow (tag, date, question_count, question_pct, unanswered_count, unanswered_pct) 
	FROM PROGRAM 'curl "https://assets.datacamp.com/production/repositories/3567/datasets/1e9257c9d86e03a979124c6d99a0ff154da953fd/stackexchange.csv"' (DELIMITER ',', FORMAT CSV, HEADER, NULL 'NA');
	
COPY fortune500
	FROM PROGRAM 'curl "https://assets.datacamp.com/production/repositories/3567/datasets/19cf8e7841e26d71feb3516c7a4b135aff8a8b4f/fortune.csv"' (DELIMITER ',', FORMAT CSV, HEADER, NULL 'NA');


				-- cast function --
-- with the cast function
select CAST (3.7 AS integer);
select CASt (total as integer) from prices;
-- without the cast function
select 3.7 :: integer;
select total :: integer from prices;

```
---
* Summarizing And Aggregating Numeric Data
<a id="summarizing-and-aggregating-numeric-data"></a>
```sql
			--- Numeric Data types and summary function--
select max(question_pct) from stackoverflow;
select min(question_pct) from stackoverflow;
-- average or mean
select avg(question_pct) from stackoverflow;
-- population variance
select var_pop(question_pct) from stackoverflow;
-- sample variance
select var_samp(question_pct) from stackoverflow;
select variance(question_pct) from stackoverflow; -- var_samp = variance
-- sample standard deviation
select stddev_samp (question_pct) from stackoverflow;
select stddev (question_pct) from stackoverflow;
-- Population standard deviation
select stddev_pop (question_pct) from stackoverflow;
-- Round
select round(32.234,2);
-- coalesce
select coalesce(value1, value2);
select coalesce(column1,column2);
select coalesce(column1,any_value);

-- Summarize by group with group by
-- PostgreSQL doesn't have a built-in round() function that accepts a double precision
select 
    tag,
    round(cast(min(question_pct) as numeric), 6) as min_pct,
    round(cast(avg(question_pct) as numeric), 6) as avg_pct,
    round(cast(max(question_pct) as numeric), 6) as max_pct
from stackoverflow
group by tag;
-- or
select 
    tag,
    round(min(question_pct)::numeric, 3) as min_pct,
    round(avg(question_pct)::numeric, 3) as avg_pct,
    round(max(question_pct)::numeric, 3) as max_pct
from stackoverflow
group by tag;

			-- Exploring Distributions--
-- count values
select
	unanswered_count, count(*)
from stackoverflow
where tag = 'amazon-ebs'
group by unanswered_count
order by unanswered_count;

--Truncate
select trunc(34.23564, 2); -- truncate and round not same
select trunc(3434.23564, -2);-- set zero before 2 decimal places

--Truncating and grouping
select
	trunc(unanswered_count, -1) as trunc_ua, 
	count(*)
from stackoverflow
where tag = 'amazon-ebs'
group by trunc_ua
order by trunc_ua;

-- Generate series
select generate_series(1,10,2);
select generate_series(0,1,.1);

--Create bins: query
with bins as(
	select 
		generate_series(30,60,5) as lower,
		generate_series(35,65,5) as upper
),ebs as(
	select
		unanswered_count
	from stackoverflow
	where tag = 'amazon-ebs'
)
select lower, upper, count(unanswered_count)
from bins
left join ebs
on unanswered_count >= lower
and unanswered_count < upper
group by lower, upper
order by lower;

			-- More summary Functions --
			
--common issues:
	--error code: 9,99,-99 somtimes 
			--function return these values which means not accurate value
	-- missing value codes: NA, NaN, N/A, #N/A
							-- 0 = IS THIS REALLY MEANS 0 OR NOT
--percentile
/*
--- find the percentile rank of the score 75.------

Imagine you have the following test scores: [45, 60, 75, 90, 95]
Steps:
    Count how many values are less than 75 → 2 values (45, 60).
    Count the total number of values → 5 values.
    Use the formula:
	Percentile=(Number of values less than X /Total values)×100
	Percentile= (2/5)×100=40%
Answer:
The score ---75 is in the-- 40th percentile, means 75 is not the 40th percentile

---- 40th percentile value for the dataset [45, 60, 75, 90, 95]----

follow these steps:
Step 1: Calculate the index
Use the formula:
	Index=(40/100×N)
	Where N = 5 (total values in the dataset):
	(40/100×5)=2
Since 2 is a whole number, we take the average of the 2nd and 3rd values (this is the rules)
Step 2: Identify values at positions 2 and 3
    Position 2 → 60
    Position 3 → 75
Step 3: Compute the average
	(60+75)2=67.5
Final Answer:
The 40th percentile value is 67.5

----
Consider the dataset [10, 20, 30, 40, 50] We want to find the 70th percentile.
Step 1: Calculate the index
	(70/100 ×5)=3.5
	Since 3.5 is NOT a whole number, we round up to 4.
Step 2: Find the value at position 4
Looking at the sorted list: Position 1 → 10 Position 2 → 20 Position 3 → 30 Position 4 → 40
Answer:
	The 70th percentile is 40 because we round up when the index is not a whole number.
*/
-- correlation function [-1,1]
select corr(assets,equity)
from fortune500;

-- median
with data as(
	select generate_series(1,5,1) as num
)
select 
	percentile_disc(.5) within group(order by num), -- return value from column
	percentile_cont(.5) within group(order by num)-- interpolates between values
from(
	select * from data
	where num not in (2)
);

			-- Creating Temporary Tables--
-- TEMP table autometically delete when disconect database
CREATE TEMP TABLE top_companies AS
select rank, title
from fortune500
where rank <=10;

-- Add more rows to the TEMP  table name top_companies
Insert into top_companies
select rank, title
from fortune500
where rank between 11 and 20;

select * from top_companies;

DROP TABLE IF EXISTS top_compaines;--delete the table

```
---
* Exploring Categorical Data And Unstructured Text
<a id="exploring-categorical-data-and-unstructured-text"></a>
```sql
			-- Character data types and common issues--
-- common issues:
	-- 'apple' != 'Apple'
	-- 'apple' != ' apple'
	-- ''		!= '  '
	-- '' 		!= NULL
	-- 'to-do' != 'to-do' -- punctuation difference

			-- Cases and spaces--
-- converting case
select  lower('aBc DeFg 7-');
select  upper('aBc DeFg 7-');

-- Case insensitive comparisons
select * from fruit where lower(fav_fruit) = 'apple';
-- Case insensitive searches
select * from fruit 
where -- also match pineapple so careful
	fav_fruit like '%apple%'; -- case sensitive
select * from fruit where fav_fruit ILIKE '%apple%'; -- case insensitive

--Trimming spaces
select trim(' abc '); -- btrim or trim, ltrim, rtrim
--Trimming other values
select trim ('hello!', '!');
select trim('Wow !', ' !wW');
select trim (lower('Wow!'), '!w')
-- trim removes char from begining,end or both but not from the middle
			
			-- Splitting and concatenating text--
-- substring
select left('tonmoy', 3), -- first 3 characters
		right('tonmoy', 3);-- last 3 characters

select left('tonmoy', 10), -- all 6 characters
		length(left('tonmoy', 10)); -- length also be 6

select substring('tonmoy' from 4 for 6); -- start 4 end at 6
--or
select substr('tonmoy', 4,6);

--Splitting on a delimiter
select split_part('Tonmoy,rashid',',',2);-- take second part of the split
select split_part('Man and woman and child',' and ', 3);-- take only child

-- Concatenatiing text
select concat('b',2,'bb');
select 'b'||2||'bb';-- all sql format
select concat('b',NULL,'bb'); -- ignore null and concat only 'b' and 'bb'
select 'b'|| NULL || 'bb'; -- if null arrive then all text become null

			-- Strategies for Multiple Transformations--
--Case when
-- Case for each of :,-,and | like -- Engineering :,- or | computer science
Select 
	case
		when category like '%: %' then split_part(category, ': ',1)
		when category like '% - %' then split_part(category, ' - ',1)
		else split_part(category, ' | ',1)
	end as major_category,
	sum(business)
from naics
group by major_category;
-- Create the table
CREATE TABLE fruit_table (
    customer INTEGER,
    fav_fruit VARCHAR(10)
);
-- Insert the data
INSERT INTO fruit_table (customer, fav_fruit) VALUES
    (349, 'apple'),
    (874, 'Apple'),
    (703, 'apple'),
    (667, 'banana'),
    (622, 'bannana'),
    (387, 'BANANA'),
    (300, 'APPLES'),
    (313, ' apple'),
    (499, ' banana'),
    (418, 'apple'),
    (841, ' BANANA'),
    (800, ' APPLE'),
    (754, 'apple');

--select * from fruit_table;
--step 1: Create temp table
CREATE TEMP TABLE recode as 
select distinct fav_fruit as original, -- original,messy values
	fav_fruit as standardized -- new standardized values but still messy
from fruit_table;

select * from recode;
select * from recode
--step 2: update values
-- All rows: lower case , remove white space on ends
update recode
	set standardized = trim(lower(original));

-- specific rows: correct a misspelling 
update recode
	set standardized = 'banana'
where standardized like '%nn%'; -- bannana
	
-- All rows: remove any s from last character
update recode
	set standardized = rtrim(standardized, 's');

--Step 3: Join original and recode tables
-- original only
select fav_fruit, count(*)
from fruit_table
group by fav_fruit;

--With recoded values
select rc.standardized, count(*)
from fruit_table as ft
left join recode as rc
on ft.fav_fruit = rc.original
group by rc.standardized;

```
---
* Working With Dates And Timestamps
<a id="working-with-dates-and-timestamps"></a>
```sql
			--date/time types and foramts--
-- main types 
	--Date: YYY-MM-DD : 2019-12-31
	--Timestamp: YYY-MM-DD HH:MM:SS : 2019-12-31 14:19:50
	--Timestamp with timezone: YYY-MM-DD HH:MM:SS+HH : 2019-12-31 14:19:50+02
-- Intervals : 7days 02:50:03

-- Date and time comparisons
-- compare with >,<,=
Select '2019-01-21' > '2018-01-01';
Select now() > '2018-01-01'; -- current timestamp
select now();
Select now() - '2018-01-01'; 

-- Date addition
select '2019-12-01'::date +1;
select '2019-12-01'::date + '1 year':: interval;
select '2019-12-01'::date + '1 year 2 days 1 hours 5 minutes':: interval;

			-- Date/time components and aggregation--
-- common date/time fields
	--fields:	century: 2019-05-03 = century 21
			  --decade : 2019-05-03 = decade 201
			  -- year, month, day
			  -- hour, minute, second
			  -- week
			  -- dow: day of week : sun as 0 and sat as 7
-- Extracting fields
select date_part('month', now()),
		extract(MONTH from now());
-- Extract to summarize by field
CREATE TABLE sales (
    date DATE,
    amt INT
);

INSERT INTO sales (date, amt) VALUES
('2010-02-14', 12),
('2010-05-03', 27),
('2010-08-19', 8);-- generate  more random rows like these

select * from sales;
-- individual sales
select * 
from sales
where date >= '2010-01-01'
and date < '2019-01-01';
-- sales by month
select 
	date_part('month', date) as month, 
	sum(amt)
from sales
group by month
order by month;
-- Truncating dates
select date_trunc('month', now());-- day can't be 0 so set to 01
-- Sales by month with year
select 
	date_trunc('month', date) as month, 
	sum(amt)
from sales
group by month
order by month;

			-- Aggregating with date/time series--
select generate_series('2019-01-01',
						'2019-01-30',
						'2 days'::interval);
select generate_series('2019-01-01',
						'2019-01-02 05:05:05',
						'5 hours'::interval);
						-- end at 2019-01-01 20:00:00 because 2019-01-02 01:00:00 > 2019-01-02 00:00:00
-- Generate series from the beginning
-- NOT GOOD IDEA
select generate_series('2019-01-31',
						'2019-12-31',
						'1 month'::interval); -- every month after feb become 28
-- GOOD IDEA subtract 1 day to get end of month
select generate_series('2019-02-01',
						'2020-01-01',
						'1 month'::interval) - '1 day'::interval;

-- Create the table
CREATE TABLE sales_ts (
    date TIMESTAMP,
    amount INTEGER
);

-- Insert the data
INSERT INTO sales_ts (date, amount) VALUES
('2018-04-23 09:13:14', 12),
('2018-04-23 13:57:53', 41),
('2018-04-23 12:05:44', 23),
('2018-04-23 09:07:33', 31),
('2018-04-23 10:31:40', 5),
('2018-04-23 09:35:16', 18),
('2018-04-23 12:17:43', 19),
('2018-04-23 12:57:49', 32),
('2018-04-23 10:12:35', 13),
('2018-04-23 13:21:30', 6);

--Normal aggeregation
-- select * from sales_ts;
select date_trunc('hour', date) as hour,
	count(*)
from sales_ts
group by hour
order by hour;

-- Aggergation with series
-- Create the series as a tble called hour_series
with hour_series as(
select generate_series('2018-04-23 09:00:00', --9am
						'2018-04-23 14:00:00', --2pm
						'1 hour':: interval) as hours
)
-- Hours form series, count date (NOT *) to count non-null
select split_part(hs.hours::text,':',1)||':00' as date_time, count(st.date)-- custom casting on timestamp
-- select to_char(hs.hours, 'HH24:MI') AS hour_display, count(st.date)
--select hs.hours as date_time, count(st.date)
from hour_series as hs
left join sales_ts as st
on hs.hours = date_trunc('hour',st.date)
group by hours
order by hours;

-- Aggregation with bins
-- Create bins
with bins as (
	select generate_series('2018-04-23 09:00:00',
							'2018-04-23 15:00:00',
							'3 hours':: interval) as lower,
		 generate_series('2018-04-23 12:00:00',
							'2018-04-23 18:00:00',
							'3 hours':: interval) as upper
)
select lower, upper,count(st.date)
from bins
left join sales_ts as st
on  st.date >= bins.lower 
and st.date  < bins.upper
group by lower, upper
order by lower

			--Time between events--
select * from sales_ts order by date;
-- how much time passes on average between each sales
-- Lead and Lag function
select date,
		lag(date) over (order by date),
		lead(date) over (order by date)
from sales_ts;

-- Time between events
select date,
	date - lag(date) over(order by date) as gap
from sales_ts;
-- Average time between events
select avg(gap)
from (
	select date,
	date - lag(date) over(order by date) as gap
from sales_ts 
)

-- Change in a time series
-- amount of sold changes one to the next
select date,
	amount,
	lag(amount) over(order by date),
	amount - lag(amount) over(order by date) as change
from sales_ts;
```
---


