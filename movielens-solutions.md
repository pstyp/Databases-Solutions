# Movielens SQL Solutions

```sql
SELECT m.title, m.release_date
FROM movies m
WHERE m.release_date BETWEEN '1983-01-01' AND '1993-12-31'
ORDER BY m.release_date DESC;
```

```sql
SELECT min_avg_ratings.title
FROM (
    SELECT DISTINCT m.id, m.title, AVG(r.rating) AS avg_rating
    FROM movies m
    JOIN ratings r ON m.id=r.movie_id
    GROUP BY m.id
    ORDER BY avg_rating
) AS min_avg_ratings
WHERE avg_rating = 1;
```

```sql
SELECT DISTINCT m.title
FROM users u
JOIN occupations o ON u.occupation_id=o.id
JOIN ratings r ON u.id=r.user_id
JOIN movies m ON r.movie_id=m.id
JOIN genres_movies gm ON gm.movie_id=m.id
JOIN genres g ON g.id=gm.genre_id
WHERE gender='M'
AND g.name='Sci-Fi'
AND o.name='Student'
AND rating=5
AND age=24;
```

```sql
SELECT DISTINCT m.title
FROM movies m
WHERE m.release_date=(
    SELECT mode.release_date
    FROM (
        SELECT m.release_date, COUNT(m.release_date) AS release_count
        FROM movies m
        GROUP BY m.release_date
        ORDER BY release_count DESC
        LIMIT 1
    ) AS mode
);
```

```sql
SELECT g.name, COUNT(m.title) AS number
FROM genres g
JOIN genres_movies gm ON (g.id=gm.genre_id)
JOIN movies m ON (m.id=gm.movie_id)
GROUP BY g.name
ORDER BY number;
```
