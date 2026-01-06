# 🧩 Case Study 01 — Advanced Subqueries

This case study focuses on **advanced subquery concepts** in Oracle SQL, covering scenarios for **Oracle Database SQL 1Z0-071** certification and real-world applications.

---

## 🔹 1) Single-row vs Multi-row Subqueries

### ❌ Common mistake

```sql
SELECT first_name
FROM employees
WHERE salary = (SELECT salary FROM employees WHERE department_id = 50);
```

> Error: ORA-01427 if more than one employee exists in department 50.

### ✅ Correct approach

```sql
SELECT first_name
FROM employees
WHERE salary IN (
  SELECT salary
  FROM employees
  WHERE department_id = 50
);
```

---

## 🔹 2) EXISTS vs IN

```sql
-- Using IN
SELECT e.employee_id
FROM employees e
WHERE e.department_id IN (
  SELECT d.department_id FROM departments d
);

-- Using EXISTS
SELECT e.employee_id
FROM employees e
WHERE EXISTS (
  SELECT 1
  FROM departments d
  WHERE d.department_id = e.department_id
);
```

> Tip: EXISTS often performs better with large datasets.

---

## 🔹 3) Correlated Subqueries

```sql
SELECT e.first_name, e.salary
FROM employees e
WHERE e.salary >
(
  SELECT AVG(salary)
  FROM employees x
  WHERE x.department_id = e.department_id
);
```

> Each employee’s salary compared to the **average salary in their own department**.

---

## 🔹 4) ANY / ALL Operator Usage

```sql
-- Find employees with salary greater than all in department 50
SELECT first_name, salary
FROM employees
WHERE salary > ALL (
  SELECT salary
  FROM employees
  WHERE department_id = 50
);

-- Find employees with salary equal to any in department 50
SELECT first_name, salary
FROM employees
WHERE salary = ANY (
  SELECT salary
  FROM employees
  WHERE department_id = 50
);
```

> Use carefully: > ALL vs > ANY changes results significantly.

---

## 🔹 5) Tips & Best Practices

- Always check if subquery returns **single or multiple rows**  
- Correlated subqueries are evaluated **row by row**  
- Prefer **EXISTS** for performance in large datasets  
- ANY / ALL operators are crucial for exam edge-case questions

---

## 📌 Next Case Study

- Case Study 02 — Advanced Joins & Edge Cases
