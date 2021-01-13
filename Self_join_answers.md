<h1>Self join - Answers</h1>
<br></br>

#### 1. How many stops are in the database.
```SQL
SELECT count ( stops.id ) AS stops
  FROM stops
```
<br></br>

#### Find the id value for the stop 'Craiglockhart'
```SQL
SELECT stops.id
  FROM stops
 WHERE stops.name = 'Craiglockhart'
```
<br></br>

#### 3. Give the id and the name for the stops on the '4' 'LRT' service.
```SQL
SELECT stops.id, stops.name
  FROM stops 
       INNER JOIN route ON (stops.id = route.stop
                            AND route.num = '4'
                            AND route.company = 'LRT')
```
<br></br>

#### 4. The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes.
```SQL
-- Given:
  SELECT company, num, count( * )
    FROM route 
   WHERE stop = 149 
         OR stop = 53
GROUP BY company, num

-- Answer:
  SELECT company, num, count( * )
    FROM route 
   WHERE stop = 149 
         OR stop = 53
GROUP BY company, num
  HAVING count( * ) = 2
```
<br></br>

#### 5. Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road.
```SQL
-- Given:
SELECT rA.company, rA.num, rA.stop, rB.stop
  FROM route rA 
       JOIN route rB ON (rA.company = rB.company AND rA.num = rB.num)
 WHERE rA.stop = 53

-- Answer:
SELECT rA.company, rA.num, rA.stop, rB.stop
  FROM route rA 
       INNER JOIN route rB ON (rA.company = rB.company AND rA.num = rB.num)
       INNER JOIN stops ON (stops.id = rB.stop
                            AND stops.name = 'London Road')
 WHERE rA.stop = 53

-- (INNER optional)
```
<br></br>

#### 6. The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross'
```SQL
-- Given:
SELECT rA.company, rA.num, stopA.name, stopB.name
  FROM route rA 
       JOIN route rB     ON (rA.company = rB.company 
                             AND rA.num = rB.num)
       JOIN stops stopA  ON (rA.stop = stopA.id)
       JOIN stops stopB  ON (rB.stop = stopB.id)
 WHERE stopA.name = 'Craiglockhart'

-- Answer:
SELECT rA.company, rA.num, stopA.name, stopB.name
  FROM route rA 
       INNER JOIN route rB     ON (rA.company = rB.company 
                                   AND rA.num = rB.num)
       INNER JOIN stops stopA  ON (rA.stop = stopA.id)
       INNER JOIN stops stopB  ON (rB.stop = stopB.id)
 WHERE stopA.name = 'Craiglockhart'
       AND stopB.name = 'London Road'

-- (INNER optional)
```
<br></br>

#### 7. Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith')
```SQL
SELECT DISTINCT startRoute.company, startRoute.num
  FROM route startRoute
       INNER JOIN route endRoute ON (startRoute.num = endRoute.num)
 WHERE startRoute.stop = 115
       AND endRoute.stop = 137
```
<br></br>

#### 8. Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'
```SQL
SELECT startRoute.company, startRoute.num
  FROM route startRoute
       INNER JOIN route endRoute   ON (startRoute.num = endRoute.num)
       INNER JOIN stops startStops ON (startRoute.stop = startStops.id)
       INNER JOIN stops endStops   ON (endRoute.stop = endStops.id)
 WHERE startStops.name =  'Craiglockhart'
       AND endStops.name = 'Tollcross'
```
<br></br>

#### 9. Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services.
```SQL
SELECT DISTINCT endStops.name, endRoute.company, endRoute.num
  FROM route startRoute
       INNER JOIN route endRoute   ON (startRoute.num = endRoute.num 
                                       AND startRoute.company = endRoute.company)
       INNER JOIN stops startStops ON (startRoute.stop = startStops.id)
       INNER JOIN stops endStops   ON (endRoute.stop = endStops.id)
 WHERE startStops.name = 'Craiglockhart'
```
<br></br>

#### 10. Find the routes involving two buses that can go from Craiglockhart to Lochend. Show the bus no. and company for the first bus, the name of the stop for the transfer, and the bus no. and company for the second bus.
```SQL
SELECT DISTINCT route1.num, route1.company, stops2.name, stops3.name, route2.num, route2.company
  FROM stops stops2
       INNER JOIN route route1 ON (route1.stop IN (stops2.id))
       INNER JOIN stops stops1 ON (stops1.id = route1.stop)
       INNER JOIN route route2 ON (route2.stop IN (stops2.id))
       INNER JOIN stops stops3 ON (stops3.id = route2.stop)
```
<br></br>