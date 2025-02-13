# Netflix Movies and TV Shows Data Analysis using SQL

![](https://github.com/najirh/netflix_sql_project/blob/main/logo.png)

## Overview
This project involves a comprehensive analysis of Netflix's movies and TV shows data using SQL. The goal is to extract valuable insights and answer various business questions based on the dataset. The following README provides a detailed account of the project's objectives, business problems, solutions, findings, and conclusions.

## Objectives

- Analyze the distribution of content types (movies vs TV shows).
- Identify the most common ratings for movies and TV shows.
- List and analyze content based on release years, countries, and durations.
- Explore and categorize content based on specific criteria and keywords.

## Dataset

The data for this project is sourced from the Kaggle dataset:

- **Dataset Link:** [Movies Dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows?resource=download)

## Schema

```sql
DROP TABLE IF EXISTS netflix;
CREATE TABLE netflix
(
    show_id      VARCHAR(5),
    type         VARCHAR(10),
    title        VARCHAR(250),
    director     VARCHAR(550),
    casts        VARCHAR(1050),
    country      VARCHAR(550),
    date_added   VARCHAR(55),
    release_year INT,
    rating       VARCHAR(15),
    duration     VARCHAR(15),
    listed_in    VARCHAR(250),
    description  VARCHAR(550)
);
```

## Business Problems and Solutions

### 1. Count the Number of Movies vs TV Shows

```sql
SELECT 
    type,
    COUNT(*)
FROM netflix
GROUP BY 1;
```

### 2. Find the Earliest and Latest Release Year

```sql
 SELECT MIN(release_year)
 AS earliest_year,
 MAX(release_year) AS latest_year
FROM netflix;
```

### 3. List All Movies Released in a Specific Year (e.g., 2020)

```sql
SELECT * 
FROM netflix
WHERE release_year = 2020;
```

### 4.  Find the Most Common Rating on Netflix

```sql
SELECT rating, COUNT(*) AS count
FROM netflix
GROUP BY rating
ORDER BY count DESC
LIMIT 1;

```

### 5. List the Top 5 Most Common Genres

```sql
SELECT listed_in, COUNT(*) AS count
FROM netflix
GROUP BY listed_in
ORDER BY count DESC
LIMIT 5;

```

### 6. Find the Total Number of TV Shows Released After 2015

```sql
SELECT COUNT(*) AS total_shows
FROM netflix
WHERE type = 'TV Show' 
AND release_year > 2015;

```


### 7. Get a List of Unique Countries in the Dataset

```sql
SELECT DISTINCT country 
FROM netflix
WHERE country IS NOT NULL;

```

### 8. Count the Number of Movies and Shows per Year

```sql
SELECT release_year, type, COUNT(*) AS count
FROM netflix
GROUP BY release_year, type
ORDER BY release_year DESC;

```


### 9. Retrieve All Content Where Cast Includes 'Leonardo DiCaprio'

```sql
SELECT * 
FROM netflix
WHERE casts LIKE '%Leonardo DiCaprio%';

```


### 10. Find All Movies Released Between 2010 and 2020

```sql
SELECT * 
FROM netflix
WHERE type = 'Movie' 
AND release_year BETWEEN 2010 AND 2020;

```

### 11. List All Movies that are Documentaries

```sql
SELECT * 
FROM netflix
WHERE listed_in LIKE '%Documentaries';
```


### 12. Find the Top 5 Directors with the Most Movies on Netflix
```sql
SELECT director, COUNT(*) AS movie_count
FROM netflix
WHERE director IS NOT NULL AND director <> ''
GROUP BY director
ORDER BY movie_count DESC
LIMIT 5;

```

### 13. Find How Many Movies Actor 'Salman Khan' Appeared in the Last 10 Years

```sql
SELECT * 
FROM netflix
WHERE casts LIKE '%Salman Khan%'
  AND release_year > EXTRACT(YEAR FROM CURRENT_DATE) - 10;
```


### 14. Find All Content That Does Not Have a Director Listed

```sql
SELECT * 
FROM netflix
WHERE director IS NULL OR director = '';

```

### 15. Find the Number of Movies Available in Each Country

```sql
SELECT country, COUNT(*) AS movie_count
FROM netflix
WHERE type = 'Movie'
GROUP BY country
ORDER BY movie_count DESC;

```

## Findings and Conclusion

- **Content Distribution:** The dataset contains a diverse range of movies and TV shows with varying ratings and genres.
- **Common Ratings:** Insights into the most common ratings provide an understanding of the content's target audience.
- **Geographical Insights:** The top countries and the average content releases by India highlight regional content distribution.
- **Content Categorization:** Categorizing content based on specific keywords helps in understanding the nature of content available on Netflix.

This analysis provides a comprehensive view of Netflix's content and can help inform content strategy and decision-making.




