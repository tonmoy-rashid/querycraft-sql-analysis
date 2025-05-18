<<<<<<< HEAD
# SQL for Data Storytelling & Decision Support

![SQL](https://img.shields.io/badge/SQL-Database-blue) ![Tutorial](https://img.shields.io/badge/Type-Tutorial-green) ![Status](https://img.shields.io/badge/Status-In%20Progress-orange)

**Author**: Tonmoy Rashid   
**Created**: 2025-04-27  
**Updated**: 2025-05-10
**Resource**: 

---
## Overview  
This repository contains comprehensive SQL tutorials and practical examples for data analysis, covering topics from basic queries to advanced analytical techniques.

## Table of Contents

1. [Data Communication Concepts](#data-communication-concepts)
	- [Fundamentals of Storytelling](#fundamentals-of-storytelling)
	- [Translating Technical Results](#translating-technical-results)
	- [Impacting the Decision Making Process](#impacting-the-decision-making-process)
2. [Data Driven Decision Making in SQL](#data-driven-decision-making-in-sql)
	- [Creating Database on PgAdmin and Importing Dataset](#creating-database-on-pgadmin-and-importing-dataset)
	- [Introduction to Business Intelligence for Online Movie Rental Database](#introduction-to-business-intelligence-for-online-movie-rental-database)
	- [Decision Making with Simple SQL Queries](#decision-making-with-simple-sql-queries)
	- [Data Driven Decision Making with Advanced SQL Queries](#data-driven-decision-making-with-advanced-sql-queries)
	- [Data Driven Decision Making with OLAP SQL Queries](#data-driven-decision-making-with-olap-sql-queries)
3. [Data Manipulation in SQL](#data-manipulation-in-sql)
	- [Prerequisite](#prerequisite)
	- [Well Take The Case](#well-take-the-case)
	- [Short and Simple Subqueries](#short-and-simple-subqueries)
	- [Correlated Queries, Nested Queries and Common Table Expressions](#correlated-queries-nested-queries-and-common-table-expressions)
	- [Window Functions](#window-functions)
4. [Exploratory Data Analysis in SQL](#exploratory-data-analysis-in-sql)
	- [Whats in the Database](#whats-in-the-database)
	- [Summarizing and Aggregating Numeric Data](#summarizing-and-aggregating-numeric-data)
	- [Exploring Categorical Data and Unstructured Text](#exploring-categorical-data-and-unstructured-text)
	- [Working with Dates and Timestamps](#working-with-dates-and-timestamps)


# Data Communication Concepts
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#data-communication-concepts) 
### Fundamentals of Storytelling
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#fundamentals-of-storytelling) 
### Translating Technical Results
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#translating-technical-results) 
### Impacting the Decision Making Process
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#impacting-the-decision-making-process) 

# Data Driven Decision Making in SQL
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#data-driven-decision-making-in-sql) 
### Creating Database on PgAdmin and Importing Dataset
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#creating-database-on-pgadmin-and-importing-dataset) 
##### **Purpose**: Create and populate the `movienow` database with movie rental data.

##### **Steps to Create the Database**
1. Create the `movienow` database.
2. Refresh the database list and select `movienow`.
3. Open the Query Tool and execute the SQL script below.
---
##### **Table: movies**
- **Purpose**: Stores information about movies available for rent.
- **Columns**: 
  - `movie_id` (Primary Key)
  - `title`
  - `genre`
  - `runtime`
  - `year_of_release`
  - `renting_price`
- **Data Import**: CSV source [link](https://assets.datacamp.com/production/repositories/4068/datasets/3eebf2a145b76fee37357bcd55ac54577c03c805/movies_181127_2.csv) 
---
##### **Table: actors**
- **Purpose**: Contains details of actors.
- **Columns**:
  - `actor_id` (Primary Key)
  - `name`
  - `year_of_birth`
  - `nationality`
  - `gender`
- **Data Import**: CSV source [link](https://assets.datacamp.com/production/repositories/4068/datasets/c67f20fa317e8229eed7586cda8bfce5fc177444/actors_181127_2.csv)

---
##### **Table: actsin**
- **Purpose**: Maps actors to movies they have acted in.
- **Columns**:
  - `actsin_id` (Primary Key)
  - `movie_id`
  - `actor_id`
- **Data Import**: CSV source [link](https://assets.datacamp.com/production/repositories/4068/datasets/6efc08575effcc9327c82fea18aaf22dfd61cc27/actsin_181127_2.csv)

---

### **Table: customers**
- **Purpose**: Stores customer details.
- **Columns**:
  - `customer_id` (Primary Key)
  - `name`
  - `country`
  - `gender`
  - `date_of_birth`
  - `date_account_start`
- **Data Import**: CSV source [link](https://assets.datacamp.com/production/repositories/4068/datasets/4b1767d8e638ab26e62d98517fef297d72260992/customers_181127_2.csv)

---
##### **Table: renting**
- **Purpose**: Tracks rental transactions.
- **Columns**:
  - `renting_id` (Primary Key)
  - `customer_id`
  - `movie_id`
  - `rating`
  - `date_renting`
- **Data Import**: CSV source [link](https://assets.datacamp.com/production/repositories/4068/datasets/d36ed7719976092a9b3387c8a2ac077914c9e1d2/renting_181127_2.csv)


### Introduction to Business Intelligence for Online Movie Rental Database
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#introduction-to-business-intelligence-for-online-movie-rental-database) 
##### **Filtering, Ordering & Aggregations in SQL**  

- **Purpose of Query 1**: Retrieve all customers from Italy  
  - **Tables Used**: `customers`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - Country: `'Italy'`  
  - **Output**: All records of customers from Italy  
  - **Use Case**: Analyzing customer demographics by country.  

- **Purpose of Query 2**: Find movies that are **not** Drama genre  
  - **Tables Used**: `movies`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - Genre: `'<> Drama'`  
  - **Output**: Movies excluding those categorized as Drama  
  - **Use Case**: Filtering movies based on genre preference.  

- **Purpose of Query 3**: Find movies with renting price **greater than or equal to** 2  
  - **Tables Used**: `movies`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - Renting Price: `>= 2`  
  - **Output**: All movies that meet the price criteria  
  - **Use Case**: Filtering movies based on pricing model.  

- **Purpose of Query 4**: Retrieve customers who started accounts between **Jan 1, 2018 and Sep 30, 2018**  
  - **Tables Used**: `customers`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - Account Start Date: `BETWEEN '2018-01-01' AND '2018-09-30'`  
  - **Output**: Customers with account start dates in the defined range  
  - **Use Case**: Analyzing customer acquisition trends.  

- **Purpose of Query 5**: Retrieve actors from **USA or Australia**  
  - **Tables Used**: `actors`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - Nationality: `IN ('USA', 'Australia')`  
  - **Output**: All actors from the selected countries  
  - **Use Case**: Identifying actors based on nationality.  

- **Purpose of Query 6**: Find rental transactions where **rating is NULL**  
  - **Tables Used**: `renting`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - Rating: `IS NULL`  
  - **Output**: Records where rating is missing  
  - **Use Case**: Understanding incomplete rating data.  

- **Purpose of Query 7**: Find rental transactions where **rating is NOT NULL**  
  - **Tables Used**: `renting`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - Rating: `IS NOT NULL`  
  - **Output**: Records where ratings are provided  
  - **Use Case**: Filtering rentals with valid ratings.  

- **Purpose of Query 8**: Retrieve **name and account start date** for customers from Italy within **specific date range**  
  - **Tables Used**: `customers`  
  - **Columns Selected**: `name`, `date_account_start`  
  - **Filters Applied**:  
    - Country: `'Italy'`  
    - Account Start Date: `BETWEEN '2018-01-01' AND '2018-09-30'`  
  - **Output**: Names and account start dates for relevant customers  
  - **Use Case**: Targeting Italian customers based on registration period.  
### Decision Making with Simple SQL Queries
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#decision-making-with-simple-sql-queries) 
##### SQL Queries for Movie Rentals & Customer Analysis

- **Purpose of Query 1**: Create a table to store selected movies with genre and renting price  
  - **Tables Created**: `movies_selected`  
  - **Columns Defined**:  
    - `title` (Movie Title)  
    - `genre` (Movie Genre)  
    - `renting_price` (Cost to rent)  
  - **Output**: Table initialized with a set of movies  
  - **Use Case**: Storing movie rental information for further analysis  

- **Purpose of Query 2**: Retrieve unique genres from the selected movies  
  - **Tables Used**: `movies_selected`  
  - **Columns Selected**: `genre`  
  - **Grouping Applied**: `GROUP BY genre`  
  - **Output**: List of distinct genres  
  - **Use Case**: Understanding genre diversity  

- **Purpose of Query 3**: Calculate the average renting price per genre  
  - **Tables Used**: `movies_selected`  
  - **Columns Selected**: `genre`, `AVG(renting_price)`  
  - **Grouping Applied**: `GROUP BY genre`  
  - **Output**: Average renting price for each genre  
  - **Use Case**: Identifying pricing trends by genre  

- **Purpose of Query 4**: Count the number of movies in each genre and round average renting price  
  - **Tables Used**: `movies_selected`  
  - **Columns Selected**: `genre`, `ROUND(AVG(renting_price),2)`, `COUNT(*)`  
  - **Grouping Applied**: `GROUP BY genre`  
  - **Output**: Genre-wise count and average renting price  
  - **Use Case**: Genre-based pricing distribution  

- **Purpose of Query 5**: Filter genres with more than two movies  
  - **Tables Used**: `movies_selected`  
  - **Columns Selected**: `genre`, `ROUND(AVG(renting_price),2)`, `COUNT(*)`  
  - **Grouping Applied**: `GROUP BY genre`  
  - **Filters Applied**: `HAVING COUNT(*) > 2`  
  - **Output**: Genres with more than two movies  
  - **Use Case**: Identifying prevalent genres  

### Data Driven Decision Making with Advanced SQL Queries
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#data-driven-decision-making-with-advanced-sql-queries) 
##### SQL Queries for Nested Queries, Correlated Queries, EXISTS, UNION, and INTERSECT

- **Purpose of Query 1**: Retrieve customer names who rated movies **≤3**  
  - **Tables Used**: `customers`, `renting`  
  - **Columns Selected**: `name`  
  - **Filters Applied**:  
    - `customer_id IN (SELECT DISTINCT customer_id FROM renting WHERE rating <= 3)`  
  - **Output**: List of customer names with low ratings  
  - **Use Case**: Identifying customers who frequently give low ratings  

- **Purpose of Query 2**: Find the earliest account start date per country, comparing it with Austria  
  - **Tables Used**: `customers`  
  - **Columns Selected**: `country`, `MIN(date_account_start)`  
  - **Grouping Applied**: `GROUP BY country`  
  - **Filters Applied**:  
    - `HAVING MIN(date_account_start) < (SELECT MIN(date_account_start) FROM customers WHERE country = 'Austria')`  
  - **Output**: Countries where the first account started earlier than Austria  
  - **Use Case**: Comparing registration trends across countries  

- **Purpose of Query 3**: Find actors who acted in the movie titled **'Ray'**  
  - **Tables Used**: `actors`, `actsin`, `movies`  
  - **Columns Selected**: `name`  
  - **Filters Applied**:  
    - `actor_id IN (SELECT actor_id FROM actsin WHERE movie_id = (SELECT movie_id FROM movies WHERE title = 'Ray'))`  
  - **Output**: List of actors featured in the movie 'Ray'  
  - **Use Case**: Finding movie-specific actor participation  

- **Purpose of Query 4**: Retrieve movies rented more than **5 times**  
  - **Tables Used**: `movies`, `renting`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - `WHERE 5 < (SELECT COUNT(*) FROM renting WHERE renting.movie_id = movies.movie_id)`  
  - **Output**: List of movies rented more than five times  
  - **Use Case**: Identifying popular movie rentals  

- **Purpose of Query 5**: Retrieve movies rented **less than** 5 times  
  - **Tables Used**: `movies`, `renting`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - `WHERE 5 > (SELECT COUNT(*) FROM renting WHERE renting.movie_id = movies.movie_id)`  
  - **Output**: List of movies rented fewer than five times  
  - **Use Case**: Finding movies with lower rental frequency  

- **Purpose of Query 6**: Retrieve movies **with at least one rating**  
  - **Tables Used**: `movies`, `renting`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - `WHERE EXISTS (SELECT * FROM renting WHERE rating IS NOT NULL AND renting.movie_id = movies.movie_id)`  
  - **Output**: List of movies that have been rated at least once  
  - **Use Case**: Identifying movies with user feedback  

- **Purpose of Query 7**: Retrieve movies **without any ratings**  
  - **Tables Used**: `movies`, `renting`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**:  
    - `WHERE NOT EXISTS (SELECT * FROM renting WHERE rating IS NOT NULL AND renting.movie_id = movies.movie_id)`  
  - **Output**: List of movies that have not been rated  
  - **Use Case**: Finding movies lacking user feedback  

- **Purpose of Query 8**: Combine **expensive movies and action-adventure movies** using `UNION` (no duplicates)  
  - **Tables Used**: `movies`  
  - **Columns Selected**: `title`, `genre`, `renting_price`  
  - **Filters Applied**:  
    - `WHERE renting_price > 2.8`  
    - `UNION` with `WHERE genre = 'Action & Adventure'`  
  - **Output**: Unique movies meeting either criterion  
  - **Use Case**: Finding high-value rentals without duplicates  

- **Purpose of Query 9**: Find the **intersection** of expensive movies and action-adventure movies  
  - **Tables Used**: `movies`  
  - **Columns Selected**: `title`, `genre`, `renting_price`  
  - **Filters Applied**:  
    - `WHERE renting_price > 2.8`  
    - `INTERSECT` with `WHERE genre = 'Action & Adventure'`  
  - **Output**: Movies that are both expensive and action-adventure  
  - **Use Case**: Analyzing overlap between pricing and genre preference  

- **Purpose of Query 10**: Combine **expensive movies and action-adventure movies** using `UNION ALL` (allows duplicates)  
  - **Tables Used**: `movies`  
  - **Columns Selected**: `title`, `genre`, `renting_price`  
  - **Filters Applied**:  
    - `WHERE renting_price > 2.8`  
    - `UNION ALL` with `WHERE genre = 'Action & Adventure'`  
  - **Output**: Movies meeting either criterion, with duplicates  
  - **Use Case**: Getting all movies matching conditions, even repeated ones  

### Data Driven Decision Making with OLAP SQL Queries
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#data-driven-decision-making-with-olap-sql-queries) 
##### OLAP Queries: CUBE, ROLLUP, GROUPING SETS

- **Purpose of Query 1**: Calculate rental counts grouped by country and genre using `CUBE`  
  - **Tables Used**: `renting`, `customers`, `movies`  
  - **Columns Selected**: `country`, `genre`, `COUNT(*) AS rental_count`  
  - **Filters Applied**:  
    - Countries: `'Austria', 'Belgium'`  
    - Genres: `'Drama', 'Comedy'`  
  - **Grouping Applied**: `GROUP BY CUBE(country, genre)`  
  - **Sorting Applied**:  
    - Prioritize fully grouped combinations  
  - **Output**: Rental count grouped by country and genre, including all possible aggregations  
  - **Use Case**: Multi-dimensional OLAP analysis  

- **Purpose of Query 2**: Calculate the number of ratings per country and genre using `CUBE`  
  - **Tables Used**: `renting`, `customers`, `movies`  
  - **Columns Selected**: `country`, `genre`, `COUNT(rating) AS rating_count`  
  - **Filters Applied**:  
    - Countries: `'Austria', 'Belgium'`  
    - Genres: `'Drama', 'Comedy'`  
  - **Grouping Applied**: `GROUP BY CUBE(country, genre)`  
  - **Sorting Applied**:  
    - Prioritize fully grouped combinations  
  - **Output**: Rating counts grouped by country and genre  
  - **Use Case**: Analyzing rating distribution across categories  

- **Purpose of Query 3**: Calculate rental counts using `ROLLUP(country, genre)`  
  - **Tables Used**: `renting`, `customers`, `movies`  
  - **Columns Selected**: `country`, `genre`, `COUNT(*) AS rental_count`  
  - **Filters Applied**:  
    - Countries: `'Austria', 'Belgium'`  
    - Genres: `'Drama', 'Comedy'`  
  - **Grouping Applied**: `GROUP BY ROLLUP(country, genre)`  
  - **Sorting Applied**:  
    - Prioritize full groupings first  
  - **Output**: Rental count including total country-level aggregations  
  - **Use Case**: Hierarchical aggregations  

- **Purpose of Query 4**: Create a view for extended rental data  
  - **View Created**: `renting_extended`  
  - **Tables Used**: `renting`, `customers`, `movies`  
  - **Columns Selected**: `renting_id`, `country`, `genre`, `rating`  
  - **Filters Applied**:  
    - Countries: `'Austria', 'Belgium'`  
    - Genres: `'Drama', 'Comedy'`  
  - **Output**: `renting_extended` view containing relevant rental details  
  - **Use Case**: Simplifying complex OLAP queries  

- **Purpose of Query 5**: Apply `GROUPING SETS` to rental data  
  - **Tables Used**: `renting_extended`  
  - **Columns Selected**: `country`, `genre`, `COUNT(*)`  
  - **Grouping Applied**: `GROUPING SETS((country, genre), (country), (genre), ())`  
  - **Output**: Rental aggregations with flexible grouping combinations  
  - **Use Case**: Analyzing multiple aggregation levels efficiently  

- **Purpose of Query 6**: Calculate rentals and average ratings grouped by country and genre  
  - **Tables Used**: `renting_extended`  
  - **Columns Selected**: `country`, `genre`, `COUNT(*)`, `ROUND(AVG(rating),2) AS avg_rating`  
  - **Grouping Applied**: `GROUPING SETS((country, genre), (genre))`  
  - **Output**: Rental and rating metrics across hierarchical dimensions  
  - **Use Case**: Deeper analytical insights  

- **Purpose of Query 7**: Identify movies with at least 4 ratings and rentals since `2018-04-01`  
  - **Tables Used**: `renting`, `customers`, `movies`  
  - **Columns Selected**: `year_of_release`, `country`, `COUNT(*) AS n_rentals`, `COUNT(DISTINCT movie_id) AS n_movies`, `ROUND(AVG(rating),2) AS avg_rating`  
  - **Filters Applied**:  
    - Rental date: `>= '2018-04-01'`  
    - Movies having at least `4` ratings  
  - **Grouping Applied**: `ROLLUP(year_of_release, country)`  
  - **Sorting Applied**:  
    - Ordered by country and year of release  
  - **Output**: Rental stats for movies meeting criteria  
  - **Use Case**: Rating-based movie popularity analysis  

# Data Manipulation in SQL
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#data-manipulation-in-sql) 
### Prerequisite
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#prerequisite) 

- **Purpose**: Set up SQLiteStudio and SQLite3 for executing queries  
  - **Software Required**:  
    - SQLiteStudio (`https://sqlitestudio.pl/`)  
    - SQLite3 (command-line tool)  

- **Installation Steps**:  
  - **Install SQLiteStudio**:  
    - Download from [SQLiteStudio](https://sqlitestudio.pl/)  
    - Run installation commands:  
      ```sh
      chmod +x SQLiteStudio-3.4.17-linux-x64-installer.run  
      ./SQLiteStudio-3.4.17-linux-x64-installer.run  
      ```  
      
  - **Install SQLite3**:  
    - Update package list:  
      ```sh
      sudo apt update  
      ```  
    - Install SQLite3:  
      ```sh
      sudo apt install sqlite3  
      ```  
    - Verify installation:  
      ```sh
      sqlite3 --version  
      ```  

- **Importing Dataset**:  
  - Open SQLiteStudio  
  - Select **'Add a database'** from the dashboard  
  - Browse for existing database file (`database.sqlite`) from local storage  
  - Click **OK** to confirm  

- **Running Queries**:  
  - Open SQLiteStudio  
  - Click **Tools → Open SQL Editor**  
  - Execute SQL queries  
  
### Well Take The Case
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#well-take-the-case) 
##### Welcome to Intermediate SQL  

- **Purpose of Query 1**: Count total matches per league  
  - **Tables Used**: `league`, `match`  
  - **Columns Selected**: `league.name`, `COUNT(country_id) AS total_match`  
  - **Join Applied**: `LEFT JOIN league ON match.country_id = league.country_id`  
  - **Grouping Applied**: `GROUP BY league.name`  
  - **Output**: Total matches played per league  
  - **Use Case**: Analyzing match volume across leagues  

- **Purpose of Query 2**: Retrieve matches played on a specific date  
  - **Tables Used**: `match`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**: `WHERE date = '2008-08-17 00:00:00'`  
  - **Limit Applied**: `LIMIT 10`  
  - **Output**: First 10 matches played on the selected date  
  - **Use Case**: Reviewing match details for a specific day  

- **Purpose of Query 3**: Retrieve match results for the **2013/2014 season**  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `id`, `home_team_goal`, `away_team_goal`  
  - **Filters Applied**: `WHERE season = '2013/2014'`  
  - **Output**: Match records showing date, home goals, and away goals  
  - **Use Case**: Filtering match results by season  

- **Purpose of Query 4**: Determine match outcome based on team goals  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `id`, `home_team_goal`, `away_team_goal`,  
    - `CASE` applied for outcome classification  
  - **Filters Applied**: `WHERE season = '2013/2014'`  
  - **Output**: Matches categorized as **home team win, away team win, or tie**  
  - **Use Case**: Simple match result classification  

- **Purpose of Query 5**: Categorize matches by date range  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `CASE WHEN date > '2015-01-01' THEN 'recent' WHEN date < '2012-01-01' THEN 'older' END AS date_category`  
  - **Output**: Matches grouped into **'recent'** or **'older'** categories  
  - **Use Case**: Date-based segmentation of matches  

- **Purpose of Query 6**: Retrieve all matches involving **Chelsea (team ID 8455)**  
  - **Tables Used**: `match`  
  - **Columns Selected**: All (`*`)  
  - **Filters Applied**: `WHERE home_team_api_id = 8455`  
  - **Limit Applied**: `LIMIT 10`  
  - **Output**: First 10 matches where Chelsea played at home  
  - **Use Case**: Reviewing Chelsea matches  

- **Purpose of Query 7**: Classify Chelsea match outcomes  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `home_team_api_id`, `away_team_api_id`,  
    - `CASE` logic for classifying wins, ties, and losses  
  - **Filters Applied**: `WHERE home_team_api_id = 8455 OR away_team_api_id = 8455`  
  - **Output**: Matches categorized based on Chelsea’s performance  
  - **Use Case**: Tracking Chelsea’s success across home and away games  

- **Purpose of Query 8**: Count Chelsea’s **home & away wins** using `CASE WHEN`  
  - **Tables Used**: `match`  
  - **Columns Selected**: `season`,  
    - `COUNT(CASE WHEN home_team_api_id = 8650 AND home_team_goal > away_team_goal THEN id END) AS home_wins`,  
    - `COUNT(CASE WHEN away_team_api_id = 8650 AND home_team_goal < away_team_goal THEN id END) AS away_wins`  
  - **Grouping Applied**: `GROUP BY season`  
  - **Output**: Win counts grouped by season  
  - **Use Case**: Summarizing Chelsea’s seasonal performance  

- **Purpose of Query 9**: Calculate Chelsea’s **total home & away goals**  
  - **Tables Used**: `match`  
  - **Columns Selected**: `season`,  
    - `SUM(CASE WHEN home_team_api_id = 8650 THEN home_team_goal END) AS home_goals`,  
    - `SUM(CASE WHEN away_team_api_id = 8650 THEN away_team_goal END) AS away_goals`  
  - **Grouping Applied**: `GROUP BY season`  
  - **Output**: Seasonal total home and away goals  
  - **Use Case**: Tracking Chelsea’s attacking strength  

- **Purpose of Query 10**: Compute **average home & away goals** per season  
  - **Tables Used**: `match`  
  - **Columns Selected**: `season`,  
    - `ROUND(AVG(CASE WHEN home_team_api_id = 8650 THEN home_team_goal END),2) AS avg_home_goals`,  
    - `ROUND(AVG(CASE WHEN away_team_api_id = 8650 THEN away_team_goal END),2) AS avg_away_goals`  
  - **Grouping Applied**: `GROUP BY season`  
  - **Output**: Average goals for home and away games per season  
  - **Use Case**: Evaluating Chelsea’s scoring efficiency  

- **Purpose of Query 11**: Compute **percentages of Chelsea home & away wins**  
  - **Tables Used**: `match`  
  - **Columns Selected**: `season`,  
    - `ROUND(AVG(CASE WHEN home_team_api_id = 8455 AND home_team_goal > away_team_goal THEN 1 WHEN home_team_api_id = 8455 AND home_team_goal < away_team_goal THEN 0 END),2) AS pct_home_wins`,  
    - `ROUND(AVG(CASE WHEN away_team_api_id = 8455 AND home_team_goal < away_team_goal THEN 1 WHEN away_team_api_id = 8455 AND home_team_goal > away_team_goal THEN 0 END),2) AS pct_away_wins`  
  - **Grouping Applied**: `GROUP BY season`  
  - **Output**: Win percentages per season for Chelsea’s home and away games  
  - **Use Case**: Measuring Chelsea’s consistency in wins  
### Short and Simple Subqueries
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#short-and-simple-subqueries) 
##### Subqueries, Nested Queries & Best Practices  

- **Purpose of Query 1**: Retrieve matches where home team goals exceed the average  
  - **Tables Used**: `match`  
  - **Columns Selected**: `home_team_goal`  
  - **Filters Applied**:  
    - `home_team_goal > (SELECT AVG(home_team_goal) FROM match)`  
  - **Output**: List of matches where home team goals are higher than the overall average  
  - **Use Case**: Identifying high-scoring matches  

- **Purpose of Query 2**: Retrieve **2012/2013 season** matches with above-average home goals  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `home_team_api_id`, `away_team_api_id`, `home_team_goal`, `away_team_goal`  
  - **Filters Applied**:  
    - `season = '2012/2013'`  
    - `home_team_goal > (SELECT AVG(home_team_goal) FROM match)`  
  - **Output**: List of matches where home team scores were above the average for the season  
  - **Use Case**: Analyzing home scoring patterns in a specific season  

- **Purpose of Query 3**: Identify teams participating in **Poland's league**  
  - **Tables Used**: `team`, `match`  
  - **Columns Selected**: `team_long_name`, `team_short_name AS abbr`  
  - **Filters Applied**:  
    - `team_api_id IN (SELECT home_team_api_id FROM match WHERE country_id = 15722)`  
  - **Output**: Teams playing in Poland's league  
  - **Use Case**: League-based team analysis  

- **Purpose of Query 4**: Find **top 3 teams** with the highest average **home goals**  
  - **Tables Used**: `match`, `team`  
  - **Columns Selected**: `team_name`, `home_avg_goal`  
  - **Filters Applied**: `season = '2011/2012'`  
  - **Grouping Applied**: `GROUP BY team_name`  
  - **Sorting Applied**: `ORDER BY home_avg_goal DESC`  
  - **Limit Applied**: `LIMIT 3`  
  - **Output**: Top 3 teams with the highest average home goals  
  - **Use Case**: Ranking teams based on home scoring efficiency  

- **Purpose of Query 5**: Count total matches & compare seasonal match count  
  - **Tables Used**: `match`  
  - **Columns Selected**: `season`, `COUNT(id) AS matches`, `(SELECT COUNT(id) FROM match) AS total_matches`  
  - **Grouping Applied**: `GROUP BY season`  
  - **Output**: Seasonal match count compared to the total number of matches  
  - **Use Case**: Understanding match distribution per season  

- **Purpose of Query 6**: Compute **goal differences** from average in **2011/2012 season**  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `(home_team_goal + away_team_goal) AS per_match_goals`, `DIFF_FROM_AVG_GOALS`  
  - **Filters Applied**: `season = '2011/2012'`  
  - **Calculations Applied**:  
    - `(home_team_goal + away_team_goal) - (SELECT AVG(home_team_goal + away_team_goal) FROM match WHERE season = '2011/2012')`  
  - **Output**: Matches showing **goal differences** compared to the seasonal average  
  - **Use Case**: Identifying high & low scoring matches  

- **Purpose of Query 7**: Demonstrate subqueries **with bad practice**  
  - **Tables Used**: `match`  
  - **Columns Selected**: `country_id`, `ROUND(AVG(matches.home_team_goal + matches.away_team_goal),2) AS avg_goals`, `overall_avg`  
  - **Filters Applied**:  
    - Season `'2013/2014'`  
    - `home_team_goal > 5`  
  - **Grouping Applied**: `GROUP BY matches.country_id`  
  - **Output**: Country-wise average match goals comparison (**with errors**)  
  - **Use Case**: Learning **why improper use of aggregates causes errors**  

- **Purpose of Query 8**: Best Practice - Using **CTEs for proper aggregation**  
  - **Tables Used**: `match`  
  - **CTEs Used**: `overall_stats`, `country_stats`  
  - **Columns Selected**: `country_id`, `avg_goals`, `overall_avg`  
  - **Filters Applied**:  
    - `season = '2013/2014'`  
    - `home_team_goal > 5`  
  - **Grouping Applied**: `GROUP BY country_id`  
  - **Final Query Uses**: `CROSS JOIN` between `overall_stats` and `country_stats`  
  - **Output**: Countries with **above-average** match goals  
  - **Use Case**: Showing **proper aggregation using CTEs**  

### Correlated Queries, Nested Queries and Common Table Expressions
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#correlated-queries-nested-queries-and-common-table-expressions) 
##### Correlated Subqueries, Nested Queries & Common Table Expressions (CTEs)

- **Purpose of Query 1**: Identify stages where **average goals** exceed the season's overall average  
  - **Tables Used**: `match`  
  - **Columns Selected**: `stage`, `ROUND(avg_goals,2) AS avg_goal`, `overall_avg`  
  - **Filters Applied**:  
    - Season: `'2012/2013'`  
    - Compare **stage-wise** averages to overall season average  
  - **Output**: Stages where scoring exceeded the season average  
  - **Use Case**: Finding high-scoring rounds in a given season  

- **Purpose of Query 2**: Use **CTEs** to improve readability and performance of the above query  
  - **Tables Used**: `match`  
  - **CTEs Used**: `overall_stat`, `stat`  
  - **Columns Selected**: `stage`, `ROUND(avg_goals,2) AS avg_goal`, `overall_avg`  
  - **Filters Applied**:  
    - Season: `'2012/2013'`  
  - **Output**: Stages ranked based on their scoring performance  
  - **Use Case**: Demonstrating **CTE-based query optimization**  

- **Purpose of Query 3**: Compare each stage’s **average goals to previous stages**  
  - **Tables Used**: `match`  
  - **Columns Selected**: `stage`, `ROUND(avg_goals,2) AS avg_goal`, `overall_avg`  
  - **Filters Applied**:  
    - Compare each stage against previous rounds  
  - **Output**: Identifies which stages had higher scoring than prior ones  
  - **Use Case**: Detect **progressive goal increases over stages**  

- **Purpose of Query 4**: Compute the **average number of goals** scored per country  
  - **Tables Used**: `country`, `match`  
  - **Columns Selected**: `country_name`, `AVG(home_team_goal + away_team_goal) AS avg_goals`  
  - **Grouping Applied**: `GROUP BY country_name`  
  - **Output**: Average match goals across different countries  
  - **Use Case**: Country-wise match scoring analysis  

- **Purpose of Query 5**: Compute **country-wise average goals using correlated subqueries**  
  - **Tables Used**: `country`, `match`  
  - **Columns Selected**: `country_name`, `avg_goals`  
  - **Filters Applied**:  
    - Match country ID **dynamically within a subquery**  
  - **Output**: Same result as Query 4, but optimized using **correlated subqueries**  
  - **Use Case**: Performance comparison between **joins and subqueries**  

- **Purpose of Query 6**: Compare **country-wise averages** to overall global average  
  - **Tables Used**: `country`, `match`  
  - **Columns Selected**: `country_name`, `avg_goals`, `avg_diff`  
  - **Filters Applied**:  
    - Calculate difference from overall match average  
  - **Output**: Countries with **above or below-average** match scores  
  - **Use Case**: Ranking countries based on scoring rates  

- **Purpose of Query 7**: Compare each **month’s total goals** to overall monthly average  
  - **Tables Used**: `match`  
  - **Columns Selected**: `month`, `SUM(home_team_goal + away_team_goal) AS total_goals`, `avg_diff`  
  - **Filters Applied**:  
    - Monthly total goals compared to the overall monthly average  
  - **Output**: Monthly goal totals with **differences from the average**  
  - **Use Case**: Identifying **high vs low scoring months**  

- **Purpose of Query 8**: Compute **seasonal average goals** for each country  
  - **Tables Used**: `country`, `match`  
  - **Columns Selected**: `country_name`, `avg_goals`  
  - **Filters Applied**:  
    - Match `country_id` dynamically  
    - Filter `season = '2011/2012'`  
  - **Output**: Seasonal **country-wise scoring trends**  
  - **Use Case**: Identifying **seasonal scoring performance**  

- **Purpose of Query 9**: Count **high-scoring matches (≥10 goals)** **without CTEs**  
  - **Tables Used**: `country`, `match`  
  - **Columns Selected**: `country_name`, `COUNT(matches.id) AS matches`  
  - **Filters Applied**:  
    - **Inner join using subqueries** to extract **high-scoring matches**  
  - **Output**: Count of matches where total goals **exceeded 10**  
  - **Use Case**: Demonstrating **subquery-based filtering**  

- **Purpose of Query 10**: Count **high-scoring matches** using **CTEs**  
  - **Tables Used**: `country`, `match`  
  - **CTEs Used**: `goal_GT10`  
  - **Columns Selected**: `country_name`, `COUNT(matches.id) AS matches`  
  - **Filters Applied**:  
    - **CTE-based data extraction**  
  - **Output**: High-scoring match count with **optimized readability**  
  - **Use Case**: Using **CTEs for better performance**  

- **Purpose of Query 11**: Compare **high vs low-scoring matches** per country  
  - **Tables Used**: `country`, `match`  
  - **CTEs Used**: `s1` (high scores), `s2` (low scores)  
  - **Columns Selected**: `country_id`, `country_name`, `COUNT(high_scores)`, `COUNT(low_scores)`  
  - **Filters Applied**:  
    - **Separate CTEs** for **high-scoring & low-scoring matches**  
    - **Ensure distinct counts to avoid duplicates**  
  - **Output**: Countries ranked by **high vs low-scoring matches**  
  - **Use Case**: Identifying **goal consistency across countries**  

### Window Functions
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#window-functions) 
##### Window Functions: Ranking, Partitioning, and Sliding Windows

- **Purpose of Query 1**: Compare **total match goals** to the overall **season average** (without window functions)  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `total_goals`, `overall_avg`  
  - **Filters Applied**:  
    - Season: `'2011/2012'`  
  - **Methods Used**:  
    - **CTE (`WITH`)** for calculating overall match average  
    - **Subqueries** for individual match comparisons  
  - **Output**: Match goal totals compared to overall season average  
  - **Use Case**: Demonstrating **non-window function method**  

- **Purpose of Query 2**: Compute **total goals per match** compared to **overall season average** (using window function)  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `total_goals`, `overall_avg`  
  - **Filters Applied**:  
    - Season: `'2011/2012'`  
  - **Window Function Used**:  
    - `AVG(home_team_goal + away_team_goal) OVER()`  
  - **Output**: Goal comparison using **window functions**  
  - **Use Case**: Optimizing previous query using window functions  

- **Purpose of Query 3**: **Rank matches** based on total goals scored  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `goals`, `rank`, `partition_rank`  
  - **Filters Applied**:  
    - Season: `'2011/2012'`  
  - **Window Functions Used**:  
    - `RANK() OVER(ORDER BY home_team_goal + away_team_goal DESC)`  
    - **Partitioning by match goal totals**  
  - **Output**: Ranked matches based on **goal counts**  
  - **Use Case**: Identifying **top goal-scoring matches**  

- **Purpose of Query 4**: Compare **match goals** to seasonal average with partitions  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `goals`, `season_avg`, `row_num`  
  - **Window Function Used**:  
    - `AVG(home_team_goal + away_team_goal) OVER(PARTITION BY season)`  
    - `ROW_NUMBER() OVER(PARTITION BY date ORDER BY date)`  
  - **Filters Applied**:  
    - Specific match dates  
  - **Output**: Seasonal comparison for **selected match dates**  
  - **Use Case**: Seasonal **goal trends across selected matches**  

- **Purpose of Query 5**: Compute **match goals & country-season average**  
  - **Tables Used**: `country`, `match`  
  - **Columns Selected**: `country_name`, `season`, `goals`, `season_ctry_avg`  
  - **Window Function Used**:  
    - `AVG(home_team_goal + away_team_goal) OVER(PARTITION BY season, country_name)`  
  - **Output**: Country-wise **goal averages per season**  
  - **Use Case**: Comparing **league-wide scoring trends**  

- **Purpose of Query 6**: Calculate **running total** of home goals (sliding window)  
  - **Tables Used**: `match`  
  - **Columns Selected**: `date`, `home_team_goal`, `running_total`  
  - **Filters Applied**:  
    - Home team ID: `Manchester City (8456)`  
    - Season: `'2011/2012'`  
  - **Window Functions Used**:  
    - `SUM(home_team_goal) OVER(ORDER BY date ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)`  
    - `SUM(home_team_goal) OVER(ORDER BY date ROWS BETWEEN 1 PRECEDING AND CURRENT ROW)`  
  - **Output**: Running total of **home goals across matches**  
  - **Use Case**: Tracking **goal trends over matches**  

- **Purpose of Query 7**: Identify **teams that defeated Manchester United** (Season: `'2013/2014'`)  
  - **Tables Used**: `match`, `team`  
  - **Columns Selected**: `team_api_id`, `team_long_name`  
  - **Filters Applied**:  
    - Manchester United loss condition  
  - **Methods Used**:  
    - **CTE (`WITH`) for loss tracking**  
    - **`CASE WHEN` filtering for losing outcomes**  
  - **Output**: Teams that **defeated Manchester United**  
  - **Use Case**: Team defeat tracking  

- **Purpose of Query 8**: Rank teams that defeated **Manchester United** based on goal count  
  - **Tables Used**: `match`, `team`  
  - **Columns Selected**: `team_api_id`, `team_long_name`, `goal_conceive`, `rank`  
  - **Filters Applied**:  
    - Manchester United loss condition  
  - **Window Function Used**:  
    - `RANK() OVER(ORDER BY goal_conceive DESC, team_long_name)`  
  - **Output**: Defeated **teams ranked by goals scored**  
  - **Use Case**: Ranking **teams based on performance against Manchester United**  

# Exploratory Data Analysis in SQL
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#exploratory-data-analysis-in-sql) 
### Whats in the Database
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#whats-in-the-database) 
##### Importing Dataset in PostgreSQL

- **Purpose**: Create and populate a PostgreSQL database with multiple tables for data analysis  
  - **Database Name**: `eda2310`  
  - **Tables Created**:  
    - `evanston311` (311 service request dataset)  
    - `company` (corporate information)  
    - `tag_company` (tag-to-company mapping)  
    - `stackoverflow` (Stack Overflow query data)  
    - `tag_type` (category types for tags)  
    - `fortune500` (top 500 global companies)  

- **Installation & Setup**:  
  - **Set timezone**: `SET TIME ZONE 'UTC';`  
  - **Refresh databases**:  
    - Right-click `Databases` → **Refresh**  
    - Right-click `eda2310` → **Select Query Tool**  
    - Execute SQL statements  

- **Creating Tables & Constraints**:  
  - **Self-referential foreign keys** (`company.parent_id`)  
  - **Primary & foreign key relationships** (`references` keyword)  
  - **Data integrity checks** (`CHECK constraints`)  

- **Data Import**:  
  - **Import CSV datasets using `COPY` command**  
  - Example:  
    ```sql
    COPY evanston311
    FROM PROGRAM 'curl "https://assets.datacamp.com/production/repositories/3567/datasets/48ea25f9557bdad445f18055f13903455189359c/ev311.csv"' 
    (DELIMITER ',', FORMAT CSV, HEADER, NULL 'NA');
    ```
  - **Imported datasets**:  
    - `evanston311.csv`
    - `stackexchange.csv`
    - `fortune.csv`  
##### Using CAST Function in SQL

- **Purpose**: Convert data types explicitly in SQL  
  - **Function Used**: `CAST()` & shorthand `::` notation  

- **Examples**:  
  - Convert **float to integer** using `CAST()`:  
    ```sql
    SELECT CAST(3.7 AS integer);
    ```  
  - Convert **column data** in a table:  
    ```sql
    SELECT CAST(total AS integer) FROM prices;
    ```  
  - Convert using shorthand `::`:  
    ```sql
    SELECT 3.7 :: integer;
    SELECT total :: integer FROM prices;
    ```  

### Summarizing and Aggregating Numeric Data
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#summarizing-and-aggregating-numeric-data) 
##### Numeric Data Types & Summary Functions  

- **Purpose of Query 1**: Retrieve **maximum, minimum, and average values** from Stack Overflow data  
  - **Tables Used**: `stackoverflow`  
  - **Columns Selected**:  
    - `MAX(question_pct)` → **Highest percentage of questions**  
    - `MIN(question_pct)` → **Lowest percentage**  
    - `AVG(question_pct)` → **Mean question percentage**  
  - **Output**: Summary statistics on question percentages  
  - **Use Case**: Understanding **question volume variations**  

- **Purpose of Query 2**: Compute **variance and standard deviation**  
  - **Tables Used**: `stackoverflow`  
  - **Columns Selected**:  
    - `VAR_POP(question_pct)` → **Population variance**  
    - `VAR_SAMP(question_pct)` → **Sample variance**  
    - `STDDEV_SAMP(question_pct)` → **Sample standard deviation**  
    - `STDDEV_POP(question_pct)` → **Population standard deviation**  
  - **Output**: Statistical dispersion of question percentages  
  - **Use Case**: Measuring **data spread for variability analysis**  

- **Purpose of Query 3**: Round numerical values  
  - **Methods Used**:  
    - `ROUND(value, decimal_places)` → **Round to specified decimals**  
  - **Output**: Rounded numerical data  
  - **Use Case**: Formatting numerical outputs  

- **Purpose of Query 4**: Handle **NULL values using `COALESCE` function**  
  - **Methods Used**:  
    - `COALESCE(value1, value2)` → **Returns first non-null value**  
  - **Output**: Replace **missing values** with alternatives  
  - **Use Case**: Ensuring **data completeness**  

---
##### Summarizing Data by Group  

- **Purpose of Query 5**: Compute **min, avg, max question percentages grouped by `tag`**  
  - **Tables Used**: `stackoverflow`  
  - **Columns Selected**: `tag`, `MIN(question_pct)`, `AVG(question_pct)`, `MAX(question_pct)`  
  - **Methods Used**:  
    - **Typecasting (`CAST AS NUMERIC`)**  
    - **Shorthand (`::numeric`)**  
  - **Grouping Applied**: `GROUP BY tag`  
  - **Output**: Tag-specific question percentage summaries  
  - **Use Case**: Tag-based **question trends analysis**  

---
##### Exploring Distributions  

- **Purpose of Query 6**: Count unanswered questions grouped by value  
  - **Tables Used**: `stackoverflow`  
  - **Columns Selected**: `unanswered_count`, `COUNT(*)`  
  - **Filters Applied**: `WHERE tag = 'amazon-ebs'`  
  - **Grouping Applied**: `GROUP BY unanswered_count`  
  - **Sorting Applied**: `ORDER BY unanswered_count`  
  - **Output**: Distribution of unanswered question counts  
  - **Use Case**: Examining **question resolution patterns**  

---
##### Truncating Data  

- **Purpose of Query 7**: Truncate values (removing decimal places instead of rounding)  
  - **Methods Used**:  
    - `TRUNC(value, decimal_places)` → **Truncates decimal precision**  
  - **Output**: Truncated numerical outputs  
  - **Use Case**: Removing **precision without rounding**  

---

##### Binning Data  

- **Purpose of Query 8**: Create **bins for unanswered questions**  
  - **Tables Used**: `stackoverflow`  
  - **CTEs Used**: `bins`, `ebs`  
  - **Methods Used**:  
    - **Generate series (`generate_series(start, end, step)`)**  
    - **Joining bins with unanswered question data**  
  - **Output**: **Grouped unanswered questions in bins**  
  - **Use Case**: **Histogram-like category analysis**  

---
##### Percentile, Correlation & Median  

- **Purpose of Query 9**: Compute **percentile ranks and values**  
  - **Methods Used**:  
    - **`percentile_disc()`** → **Discrete percentile (actual values)**  
    - **`percentile_cont()`** → **Continuous percentile (interpolated values)**  
  - **Output**: Percentile-based statistics  
  - **Use Case**: Finding **data thresholds and distributions**  

- **Purpose of Query 10**: Compute **correlation between assets & equity**  
  - **Tables Used**: `fortune500`  
  - **Columns Selected**: `CORR(assets, equity)`  
  - **Output**: Correlation coefficient (**between -1 and 1**)  
  - **Use Case**: Measuring **how asset values relate to equity**  

---
##### Creating Temporary Tables  

- **Purpose of Query 11**: Store **Fortune 500 top 10 companies in a temporary table**  
  - **Tables Used**: `fortune500`, `top_companies`  
  - **Methods Used**:  
    - `CREATE TEMP TABLE top_companies AS (SELECT rank, title FROM fortune500 WHERE rank <=10)`  
  - **Output**: Temporary storage for top-ranked companies  
  - **Use Case**: Creating **session-based data snapshots**  

- **Purpose of Query 12**: **Add more rows** to the temporary table  
  - **Methods Used**:  
    - `INSERT INTO top_companies SELECT rank, title FROM fortune500 WHERE rank BETWEEN 11 AND 20`  
  - **Output**: Extended company data  
  - **Use Case**: Expanding **temporary analysis scope**  

- **Purpose of Query 13**: **Drop temporary tables after analysis**  
  - **Methods Used**:  
    - `DROP TABLE IF EXISTS top_companies;`  
  - **Output**: Cleanup after temporary use  
  - **Use Case**: Freeing up database resources  


### Exploring Categorical Data and Unstructured Text
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#exploring-categorical-data-and-unstructured-text) 
##### Character Data Types & Common Issues

- **Purpose of Query 1**: Identify common character data issues  
  - **Common Issues**:  
    - **Case sensitivity** → `'apple' != 'Apple'`  
    - **Leading/trailing spaces** → `'apple' != ' apple'`  
    - **Empty strings vs NULL values** → `'' != NULL`  
    - **Punctuation differences** → `'to-do' != 'to–do'`  
  - **Use Case**: Ensuring **data consistency** when processing character data  

---
##### Case & Space Transformations  

- **Purpose of Query 2**: Convert text to **uppercase or lowercase**  
  - **Methods Used**:  
    - `LOWER(value)` → Convert text to **lowercase**  
    - `UPPER(value)` → Convert text to **uppercase**  
  - **Output**: Uniformly formatted text  
  - **Use Case**: Enforcing **case consistency**  

- **Purpose of Query 3**: Perform **case-insensitive comparisons**  
  - **Methods Used**:  
    - `LOWER(column) = 'apple'` → Convert values before comparison  
    - `ILIKE '%apple%'` → Case-insensitive search  
  - **Output**: Normalize case-sensitive **data lookups**  
  - **Use Case**: Improving **data matching accuracy**  

---
##### Text Splitting & Concatenation  

- **Purpose of Query 4**: Extract substrings from text  
  - **Methods Used**:  
    - `LEFT(value, num_chars)` → Extract **leftmost** characters  
    - `RIGHT(value, num_chars)` → Extract **rightmost** characters  
    - `SUBSTRING(value FROM start_pos FOR length)` → Extract portion  
  - **Output**: Extracted substrings  
  - **Use Case**: Data cleaning **for structured processing**  

- **Purpose of Query 5**: Split text using **delimiters**  
  - **Methods Used**:  
    - `SPLIT_PART(value, delimiter, part_index)` → Extract specific parts  
  - **Output**: Segmented text elements  
  - **Use Case**: Separating **compound values** (e.g., names, categories)  

- **Purpose of Query 6**: Concatenate text  
  - **Methods Used**:  
    - `CONCAT(value1, value2, ...)` → Merge text **ignoring NULLs**  
    - `"value1" || "value2"` → Alternative SQL concatenation  
  - **Output**: Constructed text strings  
  - **Use Case**: Creating **combined values**  

---
##### Multi-Transformation Strategies  

- **Purpose of Query 7**: Standardize major categories using multiple split conditions  
  - **Tables Used**: `naics`  
  - **Methods Used**:  
    - **`CASE` statements to handle multiple delimiters (`:, -, |`)**  
  - **Output**: Extracted major category names  
  - **Use Case**: Data normalization across multiple formats  

---
##### Standardizing Text via Temporary Tables  

- **Purpose of Query 8**: Create a **temporary table** for standardizing fruit names  
  - **Tables Used**: `fruit_table`, `recode`  
  - **Steps**:  
    1. **Create temporary table** → `CREATE TEMP TABLE recode AS (SELECT DISTINCT fav_fruit AS original, fav_fruit AS standardized FROM fruit_table);`  
    2. **Update standardized values** → Normalize case & trim spaces  
    3. **Correct misspellings** (`bannana → banana`)  
    4. **Remove unnecessary trailing characters**  
  - **Output**: Cleaned & standardized fruit names  
  - **Use Case**: **Data deduplication & normalization**  

---
##### Joining Original & Standardized Data  

- **Purpose of Query 9**: Compare **original vs standardized fruit names**  
  - **Tables Used**: `fruit_table`, `recode`  
  - **Methods Used**:  
    - **Aggregation (`COUNT(*)` to compute frequencies)**  
    - **Join with recoded values (`LEFT JOIN recode ON fruit_table.fav_fruit = recode.original`)**  
  - **Output**: Fruit name counts **before & after standardization**  
  - **Use Case**: Measuring **data consistency improvements**  
  
### Working with Dates and Timestamps
[Click here for code](SQL%20for%20Data%20Storytelling%20&%20Decision%20Support.md#working-with-dates-and-timestamps) 
##### Character Data Types & Common Issues

- **Purpose of Query 1**: Identify common character data issues  
  - **Common Issues**:  
    - **Case sensitivity** → `'apple' != 'Apple'`  
    - **Leading/trailing spaces** → `'apple' != ' apple'`  
    - **Empty strings vs NULL values** → `'' != NULL`  
    - **Punctuation differences** → `'to-do' != 'to–do'`  
  - **Use Case**: Ensuring **data consistency** when processing character data  

---
##### Case & Space Transformations  

- **Purpose of Query 2**: Convert text to **uppercase or lowercase**  
  - **Methods Used**:  
    - `LOWER(value)` → Convert text to **lowercase**  
    - `UPPER(value)` → Convert text to **uppercase**  
  - **Output**: Uniformly formatted text  
  - **Use Case**: Enforcing **case consistency**  

- **Purpose of Query 3**: Perform **case-insensitive comparisons**  
  - **Methods Used**:  
    - `LOWER(column) = 'apple'` → Convert values before comparison  
    - `ILIKE '%apple%'` → Case-insensitive search  
  - **Output**: Normalize case-sensitive **data lookups**  
  - **Use Case**: Improving **data matching accuracy**  

---
##### Text Splitting & Concatenation  

- **Purpose of Query 4**: Extract substrings from text  
  - **Methods Used**:  
    - `LEFT(value, num_chars)` → Extract **leftmost** characters  
    - `RIGHT(value, num_chars)` → Extract **rightmost** characters  
    - `SUBSTRING(value FROM start_pos FOR length)` → Extract portion  
  - **Output**: Extracted substrings  
  - **Use Case**: Data cleaning **for structured processing**  

- **Purpose of Query 5**: Split text using **delimiters**  
  - **Methods Used**:  
    - `SPLIT_PART(value, delimiter, part_index)` → Extract specific parts  
  - **Output**: Segmented text elements  
  - **Use Case**: Separating **compound values** (e.g., names, categories)  

- **Purpose of Query 6**: Concatenate text  
  - **Methods Used**:  
    - `CONCAT(value1, value2, ...)` → Merge text **ignoring NULLs**  
    - `"value1" || "value2"` → Alternative SQL concatenation  
  - **Output**: Constructed text strings  
  - **Use Case**: Creating **combined values**  

---
##### Multi-Transformation Strategies  

- **Purpose of Query 7**: Standardize major categories using multiple split conditions  
  - **Tables Used**: `naics`  
  - **Methods Used**:  
    - **`CASE` statements to handle multiple delimiters (`:, -, |`)**  
  - **Output**: Extracted major category names  
  - **Use Case**: Data normalization across multiple formats  

---
##### Standardizing Text via Temporary Tables  

- **Purpose of Query 8**: Create a **temporary table** for standardizing fruit names  
  - **Tables Used**: `fruit_table`, `recode`  
  - **Steps**:  
    1. **Create temporary table** → `CREATE TEMP TABLE recode AS (SELECT DISTINCT fav_fruit AS original, fav_fruit AS standardized FROM fruit_table);`  
    2. **Update standardized values** → Normalize case & trim spaces  
    3. **Correct misspellings** (`bannana → banana`)  
    4. **Remove unnecessary trailing characters**  
  - **Output**: Cleaned & standardized fruit names  
  - **Use Case**: **Data deduplication & normalization**  

---
##### Joining Original & Standardized Data  

- **Purpose of Query 9**: Compare **original vs standardized fruit names**  
  - **Tables Used**: `fruit_table`, `recode`  
  - **Methods Used**:  
    - **Aggregation (`COUNT(*)` to compute frequencies)**  
    - **Join with recoded values (`LEFT JOIN recode ON fruit_table.fav_fruit = recode.original`)**  
  - **Output**: Fruit name counts **before & after standardization**  
  - **Use Case**: Measuring **data consistency improvements**  


# Associate Data Analyst in SQL - Learning Repository

📊 A collection of SQL queries, analysis exercises, and learning notes from my data analytics journey.

## 📚 Source Attribution

This repository contains educational materials inspired by:
- **[Associate Data Analyst in SQL Career Track](https://app.datacamp.com/learn/career-tracks/associate-data-analyst-in-sql)** on DataCamp
- **[DataCamp](https://www.datacamp.com)** learning platform

### 🔍 Content Breakdown:
- **Core Exercises**: SQL solutions from DataCamp's curriculum (marked accordingly)
- **Extended Practice**: My own variations and additional challenges
- **Independent Projects**: Original analyses applying learned concepts

## ⚖️ Fair Use Declaration

1. **Educational Purpose**: Created solely for learning and skill development
2. **Content Ownership**: 
   - DataCamp retains all rights to original course materials
   - I claim authorship only for independent extensions/modifications
3. **Access Context**: Course accessed through DataCamp's platform (not individually purchased)

## 🛡️ Intellectual Property Notice

```sql
-- Example of code attribution within SQL files:
-- Concept based on DataCamp's "Associate Data Analyst" course
-- Modified/Extended by [Your Name] for learning purposes
=======
# querycraft-sql-analysis
>>>>>>> origin/main
