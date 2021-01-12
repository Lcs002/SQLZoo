<h1>SELECT within SELECT Tutorial</h1>
<br></br>

#### 1. List each country name where the population is larger than that of 'Russia'.
```SQL
SELECT name
FROM world
WHERE population > (SELECT population
                    FROM world
                    WHERE name = 'Russia')
```
<br></br>

#### 2. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
```SQL
SELECT name 
FROM world 
WHERE continent = 'Europe'
      AND gdp/population > (SELECT gdp/population
                            FROM world
                            WHERE name = 'United Kingdom')
```
<br></br>

#### 3. Name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.
```SQL
SELECT name, continent
FROM world 
WHERE continent IN (SELECT continent
                   FROM world
                   WHERE name = 'Argentina'
                         OR name = 'Australia')
```
<br></br>

#### 4. Country has a population that is more than Canada but less than Poland.
```SQL
SELECT name
FROM world 
WHERE population > (SELECT population
                    FROM world 
                    WHERE name = 'Canada')
      AND population < (SELECT population
                        FROM world
                        WHERE name = 'Poland')
```
<br></br>

#### 5. Name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
```SQL
SELECT name, concat( format( round( (population / (SELECT population
                                                   FROM world
                                                   WHERE name = 'Germany'))
                              ,2) * 100
                      ,0)
              ,'%')
FROM world
WHERE continent = 'Europe'
```
<br></br>

#### 6. Which countries have a GDP greater than every country in Europe?
```SQL
SELECT name 
FROM world
WHERE gdp > ALL( SELECT gdp
                 FROM world
                 WHERE continent = 'Europe'
                 AND gdp >= 0)
```
<br></br>

#### 7. Find the largest country (by area) in each continent, show the continent, the name and the area:
```SQL
SELECT continent, name, area
FROM world me
WHERE area >= ALL( SELECT area
                   FROM world other
                   WHERE me.continent = other.continent)
```
<br></br>

#### 8. List each continent and the name of the country that comes first alphabetically.
```SQL
SELECT continent, name
FROM world me
WHERE name <= ALL( SELECT name 
                   FROM world other
                   WHERE me.continent = other.continent)
```
<br></br>

#### 9. Continents where all countries have a population <= 25000000.
```SQL
SELECT name, continent, population 
FROM world me
WHERE 25000000 >= ALL(SELECT population
      FROM world other
      WHERE me.continent = other.continent)
```
<br></br>

#### 10. Some countries have populations more than three times that of any of their neighbours (in the same continent). Give the countries and continents.
```SQL
SELECT name, continent
FROM world me
WHERE me.population > ALL (SELECT other.population * 3
                           FROM world other
                           WHERE me.continent = other.continent
                                 AND me.name != other.name
                                 AND population != 0)
```
<br></br>