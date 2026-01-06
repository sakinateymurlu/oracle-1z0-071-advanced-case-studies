# 🧩 Case Study 04 — Date & Timestamp Nuances

This case study focuses on **advanced Date and Timestamp handling** in Oracle SQL, crucial for **1Z0-071 certification prep** and real-world time-based queries.

---

## 🔹 1) Basic Date Functions

```sql
SELECT SYSDATE, CURRENT_DATE, SYSTIMESTAMP, CURRENT_TIMESTAMP
FROM dual;
```

> SYSDATE = current date/time in DB timezone  
> CURRENT_DATE = current date in **session timezone**  
> SYSTIMESTAMP = timestamp with fractional seconds + timezone  
> CURRENT_TIMESTAMP = timestamp in **session timezone**

---

## 🔹 2) Time Zone Functions

```sql
SELECT DBTIMEZONE, SESSIONTIMEZONE FROM dual;
```

> DBTIMEZONE = database timezone  
> SESSIONTIMEZONE = current session timezone (can be altered)

---

## 🔹 3) Intervals (DATE & TIMESTAMP Arithmetic)

```sql
-- Add 1 year to hire_date
SELECT hire_date + INTERVAL '1' YEAR AS next_year
FROM employees;

-- Subtract 2 hours from current timestamp
SELECT SYSTIMESTAMP - INTERVAL '2' HOUR AS two_hours_ago
FROM dual;
```

> INTERVAL allows **precise date/time arithmetic**: YEAR TO MONTH, DAY TO SECOND.

---

## 🔹 4) Truncating & Extracting

```sql
-- Truncate to day/month/year
SELECT TRUNC(SYSDATE, 'MM') AS month_start FROM dual;

-- Extract parts
SELECT EXTRACT(YEAR FROM hire_date) AS hire_year,
       EXTRACT(MONTH FROM hire_date) AS hire_month
FROM employees;
```

> Useful for **reporting & grouping by date parts**.

---

## 🔹 5) Comparing Timestamps

```sql
SELECT *
FROM employees
WHERE hire_date BETWEEN TO_DATE('2025-01-01','YYYY-MM-DD') 
                    AND TO_DATE('2025-12-31','YYYY-MM-DD');
```

> Always use **TO_DATE / TO_TIMESTAMP** to avoid implicit conversion issues.

---

## 🔹 6) Tips & Best Practices

- Always know the **difference between SYSDATE, CURRENT_DATE, SYSTIMESTAMP, CURRENT_TIMESTAMP**  
- Use **INTERVAL types** for precise calculations  
- Time zone awareness is critical for **global applications**  
- TRUNC and EXTRACT are key for **grouping and analytics**  

---

## 📌 Next Case Study

- Case Study 05 — Set Operators & Grouping Sets
