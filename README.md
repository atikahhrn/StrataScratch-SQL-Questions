# StrataScratch-SQL-Questions
My solutions for SQL interview questions from StrataScratch

## [Dropbox: Salaries Differences](https://platform.stratascratch.com/coding/10308-salaries-differences?code_type=1)

**Write a query that calculates the difference between the highest salaries found in the marketing and engineering departments. Output just the absolute difference in salaries.**

```sql
SELECT MAX(e.salary)-
    (SELECT MAX(salary)
    FROM db_employee AS e
    INNER JOIN db_dept AS d
        ON e.department_id = d.id
    WHERE d.department = 'engineering') AS salary_difference
FROM db_employee AS e
INNER JOIN db_dept AS d
    ON e.department_id = d.id
WHERE d.department = 'marketing';
```
![image](https://user-images.githubusercontent.com/108443483/222057086-b428be4a-cc4b-4781-9d33-c07ed4a3213c.png)



