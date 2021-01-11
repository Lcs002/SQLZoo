<h1>SELECT from world Tutorial - Answers</h1>
<br></br>

#### 1. Show the name, continent and population of all countries.
```SQL
SELECT name, continent, population
FROM world;
```
<br></br>

#### 2. Show the name for the countries that have a population of at least 200 million.
```SQL
SELECT name
FROM world
WHERE population >= 200000000;
```
<br></br>

#### 3. Name and the per capita GDP for those countries with a population of at least 200 million.
```SQL
SELECT name, gdp/population
FROM world
WHERE population >= 200000000;
```
<br></br>

#### 4. Name and population in millions for the countries of the continent 'South America' (in millions).
```SQL
SELECT name, population/1000000 
FROM world
WHERE continent = 'South America';
```
<br></br>

#### 5. Name and population for France, Germany, Italy.
```SQL
SELECT name, population 
FROM world
WHERE name in ('France',
    'Germany',
    'Italy');
```
<br></br>

#### 6. Countries with the word 'United'.
```SQL
SELECT name 
FROM world
WHERE name like '%United%';
```
<br></br>

#### 7. Data of big countries. (Big IF area > 3 million OR population > 250 million).
```SQL
SELECT name, population, area 
FROM world 
WHERE area > 3000000 
    or population > 250000000;
```
<br></br>

#### 8. Data of big countries (ONLY big population OR big area).
```SQL
SELECT name, population, area 
FROM world 
WHERE population > 250000000 
    and not area > 3000000 
    or not population > 250000000 
    and area > 3000000;
```
<br></br>

#### 9. Name, population (millions) and GDP (billions) for the countries of 'South America'. (2 decimal places).
```SQL
SELECT name, round(population/1000000,2), round(gdp/1000000000,2) 
FROM world 
WHERE continent = 'South America';
```
<br></br>

#### 10. Name and per-capita GDP for countries with a GDP >= 1 trillion. (Round value to nearest 1000).
```SQL
SELECT name, round(gdp/population, -3) 
FROM world
WHERE gdp > 1000000000000;
```
<br></br>

#### 11. Country and it's capital where length of country's name and capital's are the same.
```SQL
SELECT name, capital 
FROM world 
WHERE length(capital) = length (name);
```
<br></br>

#### 12. Name and capital where the first letters match. (Don't include countries where name AND capital are the same).
```SQL
SELECT name, capital 
FROM world
WHERE left(name,1) = left(capital,1) 
    and name != capital;
```
<br></br>

#### 13. Country with all the vowels and no spaces in it's name.
```SQL
SELECT name 
FROM world 
WHERE name not like '% %' 
    and name like '%a%' 
    and name like '%e%' 
    and name like '%i%' 
    and name like '%o%' 
    and name like '%u%';
```
