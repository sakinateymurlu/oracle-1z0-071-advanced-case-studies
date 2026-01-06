# 🧩 Case Study 03 — MERGE / Upsert Scenarios

This case study focuses on **MERGE and UPSERT operations** in Oracle SQL, essential for **1Z0-071 certification prep** and real-world ETL/data integration tasks.

---

## 🔹 1) Basic MERGE (Upsert)

```sql
MERGE INTO employees t
USING staging_employees s
ON (t.employee_id = s.employee_id)
WHEN MATCHED THEN
  UPDATE SET t.salary = s.salary
WHEN NOT MATCHED THEN
  INSERT (employee_id, first_name, salary)
  VALUES (s.employee_id, s.first_name, s.salary);
```

> MERGE allows **update if exists, insert if not** in a single statement.

---

## 🔹 2) MERGE with Filter in USING

```sql
MERGE INTO sales t
USING (
  SELECT * FROM sales_staging
  WHERE load_flag = 'Y'
) s
ON (t.id = s.id)
WHEN MATCHED THEN
  UPDATE SET t.amount = s.amount;
```

> Filtering **inside USING** ensures only selected rows are merged. Avoid putting WHERE outside → affects full table.

---

## 🔹 3) INSERT ALL vs MERGE

### INSERT ALL — multiple target tables

```sql
INSERT ALL
  INTO sales_2024 VALUES (1, 'Product A', 500)
  INTO sales_audit VALUES (1, 'Product A', SYSDATE)
SELECT * FROM dual;
```

> Useful for **bulk insert into multiple tables simultaneously**.

### MERGE — Upsert (single target table)

```sql
MERGE INTO sales t
USING staging_sales s
ON (t.sales_id = s.sales_id)
WHEN MATCHED THEN
  UPDATE SET t.amount = s.amount
WHEN NOT MATCHED THEN
  INSERT (sales_id, product_name, amount)
  VALUES (s.sales_id, s.product_name, s.amount);
```

> Choose MERGE when **update+insert on a single table** is required.

---

## 🔹 4) Handling Complex Conditions

```sql
MERGE INTO employees t
USING (
  SELECT * FROM staging_employees
  WHERE status = 'ACTIVE'
) s
ON (t.employee_id = s.employee_id AND t.department_id = s.department_id)
WHEN MATCHED THEN
  UPDATE SET t.salary = s.salary;
```

> Combine multiple conditions in **ON clause** for precise row matching.

---

## 🔹 5) Tips & Best Practices

- MERGE = **UPSERT** (Update + Insert)  
- INSERT ALL = **multi-table bulk insert**  
- Always filter **inside USING** subquery for accuracy  
- Test MERGE statements on **sample data first** to avoid overwriting  

---

## 📌 Next Case Study

- Case Study 04 — Date & Timestamp Nuances
