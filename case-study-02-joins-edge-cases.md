# 🧩 Case Study 02 — Advanced Joins & Edge Cases

This case study focuses on **advanced JOIN scenarios** in Oracle SQL, designed for **1Z0-071 certification prep** and real-world reporting challenges.

---

## 🔹 1) ANSI vs Legacy Oracle Join Syntax

### Legacy (+) Join

```sql
SELECT e.first_name, d.department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id(+);
```

### ANSI JOIN (recommended)

```sql
SELECT e.first_name, d.department_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.department_id;
```

> Tip: Always prefer ANSI JOIN syntax — clearer and standard.

---

## 🔹 2) Self-Join Example

```sql
SELECT e.employee_id, e.first_name,
       m.employee_id AS manager_id, m.first_name AS manager_name
FROM employees e
JOIN employees m
ON e.manager_id = m.employee_id;
```

> Useful for **employee-manager hierarchy** or comparing rows within the same table.

---

## 🔹 3) Join + Aggregate Pitfalls

```sql
SELECT d.department_name, COUNT(e.employee_id)
FROM departments d
LEFT JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;
```

> LEFT JOIN ensures **departments with no employees** still appear with count 0.

---

## 🔹 4) Multiple Joins & Complex Filtering

```sql
SELECT e.first_name, d.department_name, l.city
FROM employees e
JOIN departments d ON e.department_id = d.department_id
JOIN locations l ON d.location_id = l.location_id
WHERE l.country_id = 'US';
```

> Multi-join queries can introduce **Cartesian product pitfalls** if ON conditions are missing.

---

## 🔹 5) Outer Join & NULL Handling

```sql
SELECT e.first_name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id
WHERE d.department_name IS NULL;
```

> Retrieves employees **without a department** — important for edge-case questions.

---

## 🔹 6) Tips & Best Practices

- Always specify **ON conditions** to prevent unwanted Cartesian joins  
- Prefer **ANSI JOIN** syntax for clarity  
- LEFT/RIGHT JOIN + aggregate → watch NULLs  
- Test multi-join queries with sample data to avoid edge-case surprises

---

## 📌 Next Case Study

- Case Study 03 — MERGE / Upsert Scenarios
