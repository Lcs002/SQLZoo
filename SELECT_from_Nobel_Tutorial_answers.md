<h1>SELECT from Nobel Tutorial</h1>
<br></br>

1. Displays Nobel prizes for 1950.
```SQL
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950;
```
<br></br>

2. Winner of the 1962 prize for Literature.
```SQL
SELECT winner
FROM nobel
WHERE yr = 1962
    and subject = 'Literature';
```
<br></br>

3. Year and subject that 'Albert Einstein' won.
```SQL
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein';
```
<br></br>

4. Name of the 'Peace' winners since 2000 included.
```SQL
SELECT winner
FROM nobel
WHERE subject = 'Peace' 
    and yr >= 2000;
```
<br></br>

5.  Data of the Literature prize winners for 1980 to 1989 inclusive.
```SQL
SELECT * 
FROM nobel
WHERE yr >= 1980 
    and yr <= 1989 
    and subject = 'Literature';
```
<br></br>

6. Data of: Theodore Roosevelt, Woodrow Wilson, Jimmy Carter, Barack Obama.
```SQL
SELECT *
FROM nobel
WHERE winner in ('Theodore Roosevelt',
    'Woodrow Wilson',
    'Jimmy Carter',
    'Barack Obama');
```
<br></br>

7. Winners with first name John.
```SQL
SELECT winner
FROM nobel
WHERE winner like 'John%';
```
<br></br>

8. Data of Physics winners for 1980 & Chemistry winners for 1984.
```SQL
SELECT *
FROM nobel
WHERE (yr = 1980 and subject = 'Physics') 
    or (yr = 1984 and subject = 'Chemistry');
```
<br></br>

9. Data of winners for 1980 excluding Chemistry and Medicine.
```SQL
SELECT *
FROM nobel
WHERE yr = 1980 
    and not subject = 'Chemistry' 
    and not subject = 'Medicine';
```
<br></br>

10. of people who won a 'Medicine' prize before 1910 excluded + winners of 'Literature' after 2004 included.
```SQL
SELECT *
FROM nobel
WHERE (yr < 1910 and subject = 'Medicine') 
    or (yr >= 2004 and subject = 'Literature');
```
<br></br>

11. Details of the prize won by PETER GRÜNBERG
```SQL
SELECT *
FROM nobel
WHERE winner = 'Peter GRÜNBERG';
```
<br></br>

12. Details of the prize won by EUGENE O'NEILL
```SQL
SELECT *
FROM nobel
WHERE winner = 'EUGENE O''NEILL';
```
<br></br>

13. Data of winners where winner starts with 'Sir' listed by most recent and name order.
```SQL
SELECT winner, yr, subject
FROM nobel
WHERE winner like 'Sir%'
ORDER BY yr desc, winner asc;
```

14. 1984 winners and subject ordered by subject and winner name. List Chemistry and Physics last.
```SQL
SELECT winner, subject
FROM nobel
WHERE yr = 1984
ORDER BY 
    CASE WHEN 
        subject IN ('Physics','Chemistry') THEN 1 ELSE 0 END,
        subject asc,
        winner asc;
```
