<h1>Using NULL - Answers</h1>
<br></br>

#### 1. List the teachers who have NULL for their department.
```SQL
SELECT teacher.name
  FROM teacher
 WHERE teacher.dept IS NULL
```
<br></br>

#### ~~ 2. Note the INNER JOIN misses the teachers with no department and the departments with no teacher. ~~
```SQL
SELECT teacher.name, dept.name
  FROM teacher 
       INNER JOIN dept ON (teacher.dept=dept.id)
```
<br></br>

#### 3. Use a different JOIN so that all teachers are listed.
```SQL
SELECT teacher.name, dept.name
  FROM teacher
       LEFT JOIN dept ON (teacher.dept = dept.id)
```
<br></br>

#### 4. Use a different JOIN so that all departments are listed.
```SQL
SELECT teacher.name, dept.name
  FROM dept
       LEFT JOIN teacher ON (teacher.dept = dept.id)
```
<br></br>

#### 5. Show teacher name and mobile number or '07986 444 2266'
```SQL
SELECT teacher.name, COALESCE( teacher.mobile, '07986 444 2266' ) AS number
  FROM teacher
```
<br></br>

#### 6. Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department.
```SQL
SELECT teacher.name, COALESCE( dept.name, 'None' ) AS dept
  FROM teacher
       LEFT JOIN dept ON (teacher.dept = dept.id)

```
<br></br>

#### 7. Use COUNT to show the number of teachers and the number of mobile phones.
```SQL
  SELECT count( teacher.id ) as teachers, count( teacher.mobile ) as mobilePhones
    FROM teacher
```
<br></br>

#### 8. Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed.
```SQL
-- USING RIGHT:
  SELECT dept.name, count( teacher.name ) AS staff
    FROM teacher 
         RIGHT JOIN dept ON (dept.id = teacher.dept)
GROUP BY dept.name

-- USING LEFT:
  SELECT dept.name, count( teacher.name ) AS staff
    FROM dept 
         LEFT JOIN teacher ON (dept.id = teacher.dept)
GROUP BY dept.name
```
<br></br>

#### 9. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise.
```SQL
SELECT teacher.name, CASE
                          WHEN teacher.dept = 1 
                               OR teacher.dept = 2
                          THEN 'Sci'
                          ELSE 'Art'
                      END type
  FROM teacher
```
<br></br>

#### 10. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise.
```SQL
SELECT teacher.name, CASE
                          WHEN teacher.dept = 1
                               OR teacher.dept = 2
                          THEN 'Sci'
                          WHEN teacher.dept = 3
                          THEN 'Art'
                          ELSE 'None'
                      END type
  FROM teacher 
```
<br></br>