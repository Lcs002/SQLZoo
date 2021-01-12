<h1>SUM and COUNT - Answers</h1>
<br></br>

#### 1. Show the total population of the world.
```SQL
SELECT SUM( population ) AS WorldPopulation 
  FROM world
```
<br></br>

#### 2. List all the continents - just once each.
```SQL
SELECT DISTINCT continent
  FROM world
```
<br></br>

#### 3. Give the total GDP of Africa
```SQL
SELECT SUM( gdp ) AS TotalGDP
  FROM world
 WHERE continent = 'Africa'
```
<br></br>

#### 4. How many countries have an area of at least 1000000
```SQL
SELEcT count( name )
  FROM world
 WHERE area >= 1000000
```
<br></br>

#### 5. What is the total population of ('Estonia', 'Latvia', 'Lithuania')?
```SQL
SELECT SUM( population ) AS TotalPopulation
  FROM world 
 WHERE name IN ('Estonia',
                'Latvia',
                'Lithuania')
```
<br></br>

#### 6. For each continent show the continent and number of countries.
```SQL
  SELECT continent, count( name ) AS nbCountries
    FROM world
GROUP BY continent
```
<br></br>

#### 7. For each continent show the continent and number of countries with populations of at least 10 million.
```SQL
  SELECT continent, count( name ) AS Countries_AtLeast_10Million
    FROM world
   WHERE population >= 10000000
GROUP BY continent
```
<br></br>

#### 8. List the continents that have a total population of at least 100 million.
```SQL
SELECT DISTINCT continent
  FROM world me
 WHERE 100000000 <= (SELECT SUM( population )
                       FROM world other
                      WHERE me.continent = other.continent)
```
<br></br>