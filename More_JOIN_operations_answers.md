<h1>More JOIN operations</h1>
<br></br>

#### 1. List the films where the yr is 1962
```SQL
SELECT id, title
  FROM movie
 WHERE yr = 1962
```
<br></br>

#### 2. When was Citizen Kane released?
```SQL
SELECT yr
  FROM movie
 WHERE title = 'Citizen Kane'
```
<br></br>

#### 3. List all of the Star Trek movies, include the id, title and yr. Order by year.
```SQL
  SELECT id, title, yr
    FROM movie me
   WHERE title LIKE '%Star Trek%'
ORDER BY yr
```
<br></br>

#### 4. What id number does the actor 'Glenn Close' have?
```SQL
SELECT id
  FROM actor
 WHERE name =  'Glenn Close'
```
<br></br>

#### 5. What is the id of the film 'Casablanca'?
```SQL
SELECT id
  FROM movie
 WHERE title = 'Casablanca'
```
<br></br>

#### 6. Obtain the cast list for 'Casablanca'.
```SQL
SELECT DISTINCT actor.name
  FROM casting 
       INNER JOIN actor ON (casting.movieid = (SELECT id
                                                 FROM movie
                                                WHERE title = 'Casablanca')
                            AND casting.actorid = actor.id)
```
<br></br>

#### 7. Obtain the cast list for the film 'Alien'
```SQL
SELECT DISTINCT actor.name
  FROM casting 
       INNER JOIN actor ON (casting.movieid = (SELECT id
                                                 FROM movie
                                                WHERE title = 'Alien')
                            AND casting.actorid = actor.id)
```
<br></br>

#### 8. List the films in which 'Harrison Ford' has appeared
```SQL
SELECT movie.title
  FROM movie 
       INNER JOIN casting ON (movie.id = casting.movieid)
       INNER JOIN actor   ON (casting.actorid = actor.id)
 WHERE actor.name =  'Harrison Ford'
```
<br></br>

#### 9. List the films where 'Harrison Ford' has appeared - but not in the starring role.
```SQL
SELECT movie.title
  FROM movie 
       INNER JOIN casting ON (movie.id = casting.movieid)
       INNER JOIN actor   ON (casting.actorid = actor.id)
 WHERE actor.name =  'Harrison Ford'
       AND casting.ord != 1
```
<br></br>

#### 10. List the films together with the leading star for all 1962 films.
```SQL
SELECT movie.title, actor.name
  FROM movie 
       INNER JOIN casting ON (movie.id = casting.movieid)
       INNER JOIN actor   ON (casting.actorid = actor.id)
 WHERE casting.ord = 1
       AND movie.yr = 1962
```
<br></br>

#### 11. Which were the busiest years for 'Rock Hudson', year, number of movies he made each year for any year in which he made more than 2 movies.
```SQL
  SELECT movie.yr, count(movie.title) AS nbMovies
    FROM movie
         INNER JOIN casting ON (movie.id = casting.movieid)
         INNER JOIN actor   ON (casting.actorid = actor.id)
   WHERE actor.name = 'Rock Hudson'
GROUP BY movie.yr
  HAVING count(movie.title) > 2
```
<br></br>

#### 12. List the film title and the leading actor for all of the films 'Julie Andrews' played in.
```SQL
SELECT movie.title, actor.name
  FROM movie 
       INNER JOIN casting ON (movie.id = casting.movieid)
       INNER JOIN actor   ON (casting.actorid = actor.id)
 WHERE movie.id IN (SELECT casting.movieid
                      FROM casting 
                           INNER JOIN actor ON (casting.actorid = actor.id)
                     WHERE actor.name = 'Julie Andrews')
       AND casting.ord = 1
```
<br></br>

#### 13. Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.
```SQL
   SELECT actor.name
     FROM actor
          INNER JOIN casting ON (actor.id = casting.actorid)
    WHERE casting.ord = 1
 GROUP BY actor.name
   HAVING count(actor.name) >= 15  
```
<br></br>

#### 14. List the films released in the year 1978 ordered by the number of actors in the cast, then by title.
```SQL
SELECT movie.title, count(actor.name) AS nbActors
    FROM movie 
         INNER JOIN casting ON (movie.id = casting.movieid)
         INNER JOIN actor   ON (casting.actorid = actor.id)
   WHERE yr = 1978
GROUP BY movie.title
ORDER BY nbActors DESC, movie.title
```
<br></br>

#### 15. List all the people who have worked with 'Art Garfunkel'.
```SQL
SELECT DISTINCT actor.name
  FROM casting 
       INNER JOIN actor ON (actor.id = casting.actorid)
       INNER JOIN movie ON (movie.id = casting.movieid)
 WHERE actor.name != 'Art Garfunkel'
       AND casting.movieid IN (SELECT casting.movieid
                                 FROM casting
                                      INNER JOIN actor ON (casting.actorid = actor.id) 
                                WHERE actor.name = 'Art Garfunkel')
```
<br></br>