# Single Row Functions (MySQL)

## Lesson Objectives
By the end of this lesson, students will be able to:
- Understand what single row functions are
- Use string, numeric, and date functions
- Apply functions on columns in the classicmodels database
- Combine functions with SQL queries
- Format and transform data for reporting

---

## 1. What are Single Row Functions?

### Concept
Single row functions:
- Operate on one row at a time
- Return one result per row

### Example
```sql
SELECT UPPER(customerName)
FROM customers;
```

---

## 2. String Functions

### Common Functions
| Function | Description |
|----------|------------|
| UPPER() | Convert to uppercase |
| LOWER() | Convert to lowercase |
| CONCAT() | Join strings |
| LENGTH() | Count characters |
| SUBSTRING() | Extract part of string |

### Examples

```sql
SELECT customerName, UPPER(customerName) AS upper_name
FROM customers;
```

```sql
SELECT CONCAT(contactFirstName, ' ', contactLastName) AS full_name
FROM customers;
```

```sql
SELECT productName, SUBSTRING(productName, 1, 5) AS short_name
FROM products;
```

---

## 3. Numeric Functions

### Common Functions
| Function | Description |
|----------|------------|
| ROUND() | Round number |
| CEIL() | Round up |
| FLOOR() | Round down |
| ABS() | Absolute value |

### Examples

```sql
SELECT productName, ROUND(buyPrice, 1) AS rounded_price
FROM products;
```

```sql
SELECT productName,
       MSRP - buyPrice AS profit,
       ROUND(MSRP - buyPrice, 2) AS rounded_profit
FROM products;
```

---

## 4. Date Functions (Detailed)

### Why Date Functions Matter
Date functions help you:
- Track business operations (orders, shipping)
- Calculate time differences
- Extract useful parts (year, month, day)
- Format dates for reports

---

### Current Date/Time Functions

| Function | Description |
|----------|------------|
| NOW() | Current date and time |
| CURDATE() | Current date only |
| CURTIME() | Current time only |

```sql
SELECT NOW(), CURDATE(), CURTIME();
```

---

### Extracting Parts of Date

| Function | Description |
|----------|------------|
| YEAR(date) | Extract year |
| MONTH(date) | Extract month |
| DAY(date) | Extract day |

```sql
SELECT orderNumber,
       YEAR(orderDate) AS year,
       MONTH(orderDate) AS month,
       DAY(orderDate) AS day
FROM orders;
```

---

### Date Difference

| Function | Description |
|----------|------------|
| DATEDIFF(date1, date2) | Returns difference in days |

```sql
SELECT orderNumber,
       DATEDIFF(shippedDate, orderDate) AS shipping_days
FROM orders;
```
 
Useful for measuring delivery performance

---

### Adding / Subtracting Dates

| Function | Description |
|----------|------------|
| DATE_ADD(date, INTERVAL x unit) | Add time |
| DATE_SUB(date, INTERVAL x unit) | Subtract time |

```sql
SELECT orderNumber,
       orderDate,
       DATE_ADD(orderDate, INTERVAL 7 DAY) AS expected_delivery
FROM orders;
```

---

### Formatting Dates

| Function | Description |
|----------|------------|
| DATE_FORMAT(date, format) | Format date output |

```sql
SELECT orderNumber,
       DATE_FORMAT(orderDate, '%d-%m-%Y') AS formatted_date
FROM orders;
```

Common formats:
- %d → Day
- %m → Month
- %Y → Year
- %W → Weekday name

---

### Handling NULL Dates

```sql
SELECT orderNumber,
       IFNULL(shippedDate, 'Pending') AS shipping_status
FROM orders;
```

---

### Real Business Example

```sql
SELECT orderNumber,
       orderDate,
       shippedDate,
       DATEDIFF(shippedDate, orderDate) AS days_taken,
       CASE 
           WHEN shippedDate IS NULL THEN 'Pending'
           WHEN DATEDIFF(shippedDate, orderDate) <= 3 THEN 'Fast'
           ELSE 'Delayed'
       END AS shipping_status
FROM orders;
```

---

## 5. Conversion & Null Functions

### Common Functions
| Function | Description |
|----------|------------|
| IFNULL() | Replace NULL |
| COALESCE() | First non-null value |

---

## 🔗 6. Using Multiple Functions Together

```sql
SELECT 
    UPPER(CONCAT(contactFirstName, ' ', contactLastName)) AS full_name,
    LENGTH(customerName) AS name_length
FROM customers;
```

---

## 7. Practice Activities

### Beginner
1. Extract year from orderDate  
2. Show current date  
3. Format orderDate as DD-MM-YYYY  

### Intermediate
1. Calculate days between order and shipping  
2. Add 5 days to orderDate  
3. Show month and year separately  

### Advanced
1. Categorize orders as Fast/Delayed  
2. Replace NULL shipped dates  
3. Create expected delivery date  

---

## 8. Quiz Questions

1. What does DATEDIFF() return?  
2. Difference between NOW() and CURDATE()?  
3. How to extract year from a date?  
4. What is DATE_FORMAT() used for?  
5. How to handle NULL dates?  

---
