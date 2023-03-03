# StrataScratch-SQL-Questions
My solutions for SQL interview questions from StrataScratch

## [Dropbox: Salaries Differences (Easy)](https://platform.stratascratch.com/coding/10308-salaries-differences?code_type=1)

**Write a query that calculates the difference between the highest salaries found in the marketing and engineering departments. Output just the absolute difference in salaries.**

```sql
--Method 1
SELECT MAX(e.salary)-
    (SELECT MAX(salary)
    FROM db_employee AS e
    INNER JOIN db_dept AS d
        ON e.department_id = d.id
    WHERE d.department = 'engineering') AS salary_differences
FROM db_employee AS e
INNER JOIN db_dept AS d
    ON e.department_id = d.id
WHERE d.department = 'marketing';
```
```sql
--Method 2
SELECT
    MAX(CASE WHEN d.department = 'marketing' THEN salary END)-
    MAX(CASE WHEN d.department = 'engineering' THEN salary END) AS salary_differences
FROM db_employee AS e
INNER JOIN db_dept AS d
    ON e.department_id = d.id;
```

![image](https://user-images.githubusercontent.com/108443483/222057086-b428be4a-cc4b-4781-9d33-c07ed4a3213c.png)

## [Salesforce: Average Salaries (Easy)](https://platform.stratascratch.com/coding/9917-average-salaries?code_type=1)

**Compare each employee's salary with the average salary of the corresponding department. Output the department, first name, and salary of employees along with the average salary of that department.**

```sql
SELECT    
    department,
    first_name,
    salary,
    AVG(salary) OVER(PARTITION BY department) AS avg
FROM employee;
```
*Solution showing the first five rows*

![image](https://user-images.githubusercontent.com/108443483/222607436-b784a5e8-520a-4e22-afd6-3ae6fdad91c4.png)

## [Amazon: Order Details (Easy)](https://platform.stratascratch.com/coding/9913-order-details?code_type=1)

**Find order details made by Jill and Eva. Consider the Jill and Eva as first names of customers. Output the order date, details and cost along with the first name. Order records based on the customer id in ascending order.**

```sql
SELECT
    c.first_name,
    o.order_date,
    o.order_details,
    o.total_order_cost
FROM customers AS c
JOIN orders AS o
    ON c.id = o.cust_id
WHERE first_name IN ('Jill', 'Eva')
ORDER BY c.id;
```
*Solution showing the first five rows*

![image](https://user-images.githubusercontent.com/108443483/222607892-78b4c326-82da-4288-9628-eeada63fe2de.png)

## [Airbnb: Number Of Bathrooms And Bedrooms (Easy)](https://platform.stratascratch.com/coding/9622-number-of-bathrooms-and-bedrooms?code_type=1)

**Find the average number of bathrooms and bedrooms for each city’s property types. Output the result along with the city name and the property type.**

```sql
SELECT
    city,
    property_type,
    AVG(bathrooms) AS n_bathrooms_avg,
    AVG(bedrooms) AS n_bedrooms_avg
FROM airbnb_search_details
GROUP BY city, property_type;
```
*Solution showing the first five rows*

![image](https://user-images.githubusercontent.com/108443483/222608762-71f39b53-8681-4932-b30e-0f49ccd4ef80.png)

