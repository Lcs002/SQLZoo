<h1>The JOIN operation - Answers</h1>
<br></br>

#### 1. Show the matchid and player name for all goals scored by Germany.
```SQL
SELECT goal.matchid, goal.player
  FROM goal
 WHERE goal.teamid = 'GER'
```
<br></br>

#### 2. Show id, stadium, team1, team2 for just game 1012.
```SQL
SELECT game.id, game.stadium, game.team1, game.team2
  FROM game
 WHERE game.id = 1012
```
<br></br>

#### 3. Show the player, teamid, stadium and mdate for every German goal.
```SQL
SELECT goal.player, goal.teamid, game.stadium, game.mdate
  FROM goal 
       INNER JOIN game ON (goal.matchid = game.id
                                AND goal.teamid = 'GER')
```
<br></br>

#### 4. Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'.
```SQL
SELECT game.team1, game.team2, goal.player
  FROM game 
       INNER JOIN goal ON (game.id = goal.matchid
                           AND goal.player like 'Mario%')
```
<br></br>

#### 5. Show player, teamid, coach, gtime for all goals scored in the first 10 minutes.
```SQL
SELECT goal.player, goal.teamid, eteam.coach, goal.gtime
  FROM goal 
       INNER JOIN eteam ON (goal.teamid = eteam.id
                            AND goal.gtime <= 10)
```
<br></br>

#### 6. Dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.
```SQL
SELECT game.mdate, eteam.teamname
  FROM game 
       INNER JOIN eteam ON (game.team1 = eteam.id
                            AND eteam.coach = 'Fernando Santos')
```
<br></br>

#### 7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'.
```SQL
SELECT goal.player
  FROM goal 
       INNER JOIN game ON (goal.matchid = game.id 
                           AND game.stadium =  'National Stadium, Warsaw')
```
<br></br>

#### 8. Show the name of all players who scored a goal against Germany.
```SQL
SELECT DISTINCT goal.player
  FROM game 
       INNER JOIN goal ON (goal.matchid = game.id 
                           AND goal.teamid != 'GER' 
                           AND (game.team1 = 'GER' OR game.team2 = 'GER'))
```
<br></br>

#### 9. Show teamname and the total number of goals scored.
```SQL
  SELECT max( eteam.teamname ), count( eteam.teamname ) AS GOLS
    FROM eteam 
         INNER JOIN goal ON (eteam.id = goal.teamid)
GROUP BY eteam.teamname
```
<br></br>

#### 10. Show the stadium and the number of goals scored in each stadium.
```SQL
  SELECT game.stadium, count(game.stadium) AS GOLS
    FROM game 
         INNER JOIN goal ON (game.id = goal.matchid)
GROUP BY game.stadium
```
<br></br>

#### 11. For every match involving 'POL', show the matchid, date and the number of goals scored.
```SQL
  SELECT goal.matchid, game.mdate, count( * ) AS GOLS
    FROM game 
         INNER JOIN goal ON (game.id = goal.matchid
                             AND (game.team1 = 'POL' OR game.team2 = 'POL'))
GROUP BY goal.matchid, game.mdate
```
<br></br>

#### 12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'.
```SQL
  SELECT goal.matchid, game.mdate, count( * ) AS GOLS
    FROM game 
         INNER JOIN goal ON (game.id = goal.matchid
                             AND goal.teamid = 'GER')
GROUP BY goal.matchid, game.mdate
```
<br></br>

#### 13. Sort your result by mdate, matchid, team1 and team2.
```SQL
  SELECT game.mdate,
         game.team1,
         sum(
             CASE 
                 WHEN goal.teamid = game.team1 
                 THEN 1
                 ELSE 0 
             END) 
         score1,
         game.team2,
         sum(
             CASE
                 WHEN goal.teamid = game.team2 
                 THEN 1 
                 ELSE 0 
             END) 
         score2
    FROM game 
         LEFT JOIN goal ON (goal.matchid = game.id)
GROUP BY game.mdate, game.team1, game.team2
ORDER BY game.mdate, goal.matchid, game.team1, game.team2
```