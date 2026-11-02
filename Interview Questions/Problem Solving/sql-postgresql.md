# 🗄️ SQL / PostgreSQL — Interview Bank (Problem Solving)

> Your resume lists **PostgreSQL + RDS**. DevOps/backend-adjacent rounds still test SQL. Try each WITHOUT looking, then check. 🟢 basic · 🟡 mid · 🔴 advanced · 🔥 common.
> Schema used below: `employees(id, name, dept_id, manager_id, salary, hire_date)`, `departments(id, name)`.

---

## A. JOINs & basics 🔥
1. 🟢🔥 `[GEN]` Difference between INNER, LEFT, RIGHT, FULL OUTER JOIN.
2. 🟢🔥 `[TCS][INFY]` List all employees with their department name.
3. 🟡 `[CTS]` Find employees who have **no** department (NULL dept).
4. 🟢 `[WIPRO]` Difference between `WHERE` and `HAVING`.
5. 🟡 `[CAPG]` `UNION` vs `UNION ALL`.
6. 🟢 `[HEXA]` `DELETE` vs `TRUNCATE` vs `DROP`.
7. 🟡 `[INFY]` Primary key vs unique key vs foreign key.
8. 🟢 `[TCS]` `IN` vs `EXISTS` — which and when?

<details><summary>Answers</summary>

```sql
-- 2
SELECT e.name, d.name FROM employees e JOIN departments d ON e.dept_id = d.id;
-- 3
SELECT * FROM employees WHERE dept_id IS NULL;      -- or LEFT JOIN ... WHERE d.id IS NULL
```
- **1** INNER=match both; LEFT=all left + matched right; RIGHT=all right; FULL=all both (NULLs where no match).
- **4** WHERE filters rows before grouping; HAVING filters groups after `GROUP BY`.
- **5** UNION removes duplicates (sorts); UNION ALL keeps all (faster).
- **6** DELETE row-by-row (logged, rollback, WHERE); TRUNCATE all rows fast (no WHERE); DROP removes the table.
- **7** PK = unique + not null + one per table; UNIQUE = unique, allows one NULL, many per table; FK = references another table's PK.
- **8** EXISTS stops at first match (good for large subqueries/correlated); IN good for small static lists.
</details>

---

## B. Aggregation & GROUP BY 🔥
9. 🟡🔥 `[CTS][WMT]` Count employees per department.
10. 🟡 `[INFY]` Departments with more than 5 employees.
11. 🟡🔥 `[TCS]` Average salary per department, highest first.
12. 🟡 `[ACN]` Total salary spend per department including departments with zero employees.
13. 🟡 `[CMCST]` Count distinct managers.

<details><summary>Answers</summary>

```sql
-- 9
SELECT dept_id, COUNT(*) FROM employees GROUP BY dept_id;
-- 10
SELECT dept_id FROM employees GROUP BY dept_id HAVING COUNT(*) > 5;
-- 11
SELECT dept_id, AVG(salary) a FROM employees GROUP BY dept_id ORDER BY a DESC;
-- 12 (LEFT JOIN so empty depts show)
SELECT d.name, COALESCE(SUM(e.salary),0) FROM departments d
LEFT JOIN employees e ON e.dept_id = d.id GROUP BY d.name;
-- 13
SELECT COUNT(DISTINCT manager_id) FROM employees;
```
</details>

---

## C. Nth highest / ranking 🔥🔥 (asked constantly)
14. 🟡🔥 `[TCS][INFY][CTS]` 2nd highest salary.
15. 🟡🔥 `[WMT]` Nth highest salary (parameterized).
16. 🟡🔥 `[PP]` Top 3 earners **per department**.
17. 🟡 `[AMZN]` Dense rank vs rank vs row_number — show the difference.
18. 🔴 `[WMT]` Median salary per department.

<details><summary>Answers</summary>

```sql
-- 14
SELECT DISTINCT salary FROM employees ORDER BY salary DESC OFFSET 1 LIMIT 1;
-- or
SELECT MAX(salary) FROM employees WHERE salary < (SELECT MAX(salary) FROM employees);
-- 15 (Nth): OFFSET N-1 LIMIT 1 on DISTINCT salaries
-- 16
SELECT * FROM (
  SELECT *, DENSE_RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) r
  FROM employees) t WHERE r <= 3;
-- 17
SELECT name, salary,
  ROW_NUMBER() OVER (ORDER BY salary DESC) rn,  -- 1,2,3,4 (unique)
  RANK()       OVER (ORDER BY salary DESC) rk,  -- 1,2,2,4 (gaps)
  DENSE_RANK() OVER (ORDER BY salary DESC) dr   -- 1,2,2,3 (no gaps)
FROM employees;
-- 18
SELECT dept_id, PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY salary) med
FROM employees GROUP BY dept_id;
```
</details>

---

## D. Duplicates 🔥
19. 🟡🔥 `[CTS][INFY]` Find duplicate emails in a `users(email)` table.
20. 🟡🔥 `[WMT]` Delete duplicates keeping the lowest id.
21. 🟡 `[ACN]` Find rows that appear more than once across all columns.

<details><summary>Answers</summary>

```sql
-- 19
SELECT email, COUNT(*) FROM users GROUP BY email HAVING COUNT(*) > 1;
-- 20 (Postgres ctid trick, or by id)
DELETE FROM users a USING users b
WHERE a.email = b.email AND a.id > b.id;
-- 21
SELECT col1,col2, COUNT(*) FROM t GROUP BY col1,col2 HAVING COUNT(*) > 1;
```
</details>

---

## E. Subqueries & self-join 🔥
22. 🟡 `[INFY]` Employees earning more than the company average.
23. 🟡🔥 `[WMT]` Employees earning more than their department average (correlated).
24. 🟡🔥 `[PP]` Employees who earn more than their manager (self-join).
25. 🟡 `[CMCST]` Departments where no employee earns > 100k.

<details><summary>Answers</summary>

```sql
-- 22
SELECT * FROM employees WHERE salary > (SELECT AVG(salary) FROM employees);
-- 23
SELECT * FROM employees e WHERE salary > (
  SELECT AVG(salary) FROM employees WHERE dept_id = e.dept_id);
-- 24
SELECT e.name FROM employees e JOIN employees m ON e.manager_id = m.id
WHERE e.salary > m.salary;
-- 25
SELECT d.name FROM departments d WHERE NOT EXISTS (
  SELECT 1 FROM employees e WHERE e.dept_id = d.id AND e.salary > 100000);
```
</details>

---

## F. Window functions 🔥 (mid/senior)
26. 🟡🔥 `[AMZN][WMT]` Running total of salary ordered by hire_date.
27. 🟡 `[PP]` Each employee's salary vs the previous hire (LAG).
28. 🟡 `[CMCST]` Difference between a row's salary and the dept max.
29. 🔴 `[AMZN]` Cumulative distribution / percent rank of salaries.
30. 🟡 `[WMT]` First and last hire per department.

<details><summary>Answers</summary>

```sql
-- 26
SELECT name, SUM(salary) OVER (ORDER BY hire_date) running FROM employees;
-- 27
SELECT name, salary, LAG(salary) OVER (ORDER BY hire_date) prev FROM employees;
-- 28
SELECT name, MAX(salary) OVER (PARTITION BY dept_id) - salary gap FROM employees;
-- 30
SELECT DISTINCT dept_id,
  FIRST_VALUE(name) OVER (PARTITION BY dept_id ORDER BY hire_date) first_hire,
  LAST_VALUE(name)  OVER (PARTITION BY dept_id ORDER BY hire_date
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) last_hire
FROM employees;
```
</details>

---

## G. Dates, strings, NULLs
31. 🟡 `[TCS]` Employees hired in the last 30 days.
32. 🟡 `[INFY]` Count hires per year.
33. 🟢 `[CTS]` Handle NULL salary as 0 in a sum. (`COALESCE`)
34. 🟡 `[WIPRO]` Extract year/month from a date.
35. 🟡 `[HEXA]` Concatenate first and last name.

<details><summary>Answers</summary>

```sql
-- 31
SELECT * FROM employees WHERE hire_date >= CURRENT_DATE - INTERVAL '30 days';
-- 32
SELECT EXTRACT(YEAR FROM hire_date) yr, COUNT(*) FROM employees GROUP BY yr;
-- 33
SELECT SUM(COALESCE(salary,0)) FROM employees;
-- 35
SELECT first_name || ' ' || last_name FROM employees;  -- or CONCAT()
```
</details>

---

## H. Concepts (vocal) 🔥
36. 🟢🔥 `[GEN]` What is an index? Clustered vs non-clustered. When does an index hurt?
37. 🔴🔥 `[WMT][PP]` Explain ACID. What are isolation levels and the anomalies they prevent?
38. 🔴 `[PP]` Optimistic vs pessimistic locking — which for payments?
39. 🟡🔥 `[INFY]` Normalization vs denormalization. Explain 1NF/2NF/3NF.
40. 🔴🔥 `[WMT]` How do you optimize a slow query? (EXPLAIN ANALYZE, indexes, N+1)
41. 🟡 `[CTS]` Stored procedure vs function vs view.
42. 🔴 `[PP]` How do you handle a deadlock?
43. 🟡 `[CMCST]` What is a transaction? COMMIT/ROLLBACK/SAVEPOINT.
44. 🟡 `[ACN]` CTE (`WITH`) vs subquery — readability/recursion.
45. 🔴 `[AMZN]` SQL vs NoSQL — when RDS vs DynamoDB?

<details><summary>Key answers</summary>

- **36 Index:** B-tree structure speeding lookups. Clustered = table physically sorted by key (one per table); non-clustered = separate structure with pointers. Hurts on write-heavy tables (every insert/update maintains it) and low-cardinality columns.
- **37 ACID:** Atomicity, Consistency, Isolation, Durability. Isolation levels: Read Uncommitted → Read Committed → Repeatable Read → Serializable; prevent dirty read, non-repeatable read, phantom read respectively.
- **38 Locking:** Optimistic = assume no conflict, check version on commit (good for low contention); pessimistic = lock rows up front (good for high contention/payments — but watch deadlocks).
- **39 Normalization:** remove redundancy. 1NF atomic values; 2NF no partial dependency on part of a composite key; 3NF no transitive dependency. Denormalize for read performance.
- **40 Slow query:** `EXPLAIN ANALYZE` → look for seq scans on big tables → add indexes, avoid `SELECT *`, fix N+1, limit rows, rewrite subquery as join.
- **42 Deadlock:** two txns wait on each other's locks; DB kills one. Avoid by consistent lock ordering, short transactions, lower isolation where safe.
</details>

---

## I. DevOps-flavored DB (RDS) 🔥
46. 🟡🔥 `[WMT]` How do you do a zero-downtime schema migration?
47. 🟡 `[PP]` How do you back up and restore RDS? (snapshots, PITR)
48. 🟡 `[CTS]` Multi-AZ vs Read Replica (again — for scaling vs HA).
49. 🟡 `[AMZN]` How do you rotate DB credentials with no downtime? (Secrets Manager)
50. 🔴 `[CMCST]` How do you monitor DB performance? (Performance Insights, slow query log, CloudWatch)

<details><summary>Key answers</summary>

- **46:** Backward-compatible migrations — add nullable column → deploy code writing both → backfill → switch reads → drop old. Use expand/contract pattern; avoid locking `ALTER` on large tables (use `pg_repack`/online DDL).
- **47:** Automated daily snapshots + transaction logs enable Point-In-Time Recovery; manual snapshots for retention; restore creates a new instance.
- **49:** Store creds in Secrets Manager with rotation Lambda; app reads from Secrets Manager; dual-user rotation avoids downtime.
</details>

---
💡 Must-memorize for any SQL round: **Nth highest, duplicates, dept-average, window ranking, JOIN types, ACID, index trade-offs.**
