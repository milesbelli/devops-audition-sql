# Devops Challenges 5 and 5A
For challenge 5, we set up the database as follows:

* Create a table of employee departments
* Create a table for employees with their departments, linked to department table
* Add departments to the department table
* Add employees into the employee table
* Query to get average salaries by city
* Query to get current server time

For challenge 5A, we run an `EXPLAIN` on the average salary query.

```
+----+-------------+------------+------------+------+---------------+--------------+---------+-----------------------------------+------+----------+---------------------------------+
| id | select_type | table      | partitions | type | possible_keys | key          | key_len | ref                               | rows | filtered | Extra                           |
+----+-------------+------------+------------+------+---------------+--------------+---------+-----------------------------------+------+----------+---------------------------------+
|  1 | SIMPLE      | department | NULL       | ALL  | PRIMARY       | NULL         | NULL    | NULL                              |   10 |   100.00 | Using temporary; Using filesort |
|  1 | SIMPLE      | employee   | NULL       | ref  | DepartmentId  | DepartmentId | 5       | ezops_sql.department.DepartmentId |    1 |   100.00 | NULL                            |
+----+-------------+------------+------------+------+---------------+--------------+---------+-----------------------------------+------+----------+---------------------------------+
2 rows in set, 1 warning (0.00 sec)
```
This indicates we are sorting the department table and then matching the corresponding `DepartmentId` column in the employee table.

To handle a scenario with 1 million rows, it would be beneficial to place an INDEX on the `DepartmentId` column, as this would speed up the search.