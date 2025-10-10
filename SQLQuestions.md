1. Nth Highest Salary and which is less then max
```
-- 2nd highest salary
SELECT TOP 1 Salary
FROM Employee
WHERE --Salary < (SELECT MAX(Salary) FROM Employee)
ORDER BY Salary DESC;

SELECT Salary
FROM (
    SELECT Salary, ROW_NUMBER() OVER (ORDER BY Salary DESC) AS rn
    FROM Employee
) AS T
WHERE rn = 2;

--- Using DENSE_RANK() (handles ties)
SELECT Salary
FROM (
    SELECT Salary, DENSE_RANK() OVER (ORDER BY Salary DESC) AS rnk
    FROM Employee
) AS T
WHERE rnk = 2;


```   
