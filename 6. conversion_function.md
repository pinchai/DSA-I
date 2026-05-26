# Conversion Functions

------------------------------------------------------------------------

## Lesson Objectives

-   Explain implicit vs explicit conversion
-   Convert between String, Number, and Date
-   Use CAST(), CONVERT(), STR_TO_DATE(), DATE_FORMAT()
-   Apply conversions in real-world queries using classicmodels

------------------------------------------------------------------------

## 1. Data Type Conversion

### Implicit Conversion (Automatic)

``` sql
SELECT '10' + 5; -- Result: 15
```

### Explicit Conversion (Manual)

``` sql
SELECT CAST('10' AS SIGNED);
```

✔ Safer and predictable

------------------------------------------------------------------------

## 2. CAST()

### Syntax

``` sql
CAST(expression AS datatype)
```

### Supported Types

-   SIGNED
-   UNSIGNED
-   DECIMAL(M,D)
-   CHAR
-   DATE
-   DATETIME

### Examples

``` sql
SELECT CAST('123' AS SIGNED);
SELECT CAST('123.45' AS DECIMAL(10,2));
SELECT CAST(500 AS CHAR);
SELECT CAST('2026-03-20' AS DATE);
```

### Edge Case

``` sql
SELECT CAST('ABC' AS SIGNED); -- Result: 0
```

### classicmodels Example

``` sql
SELECT 
    customerNumber,
    customerName,
    CAST(creditLimit AS CHAR) AS credit_text
FROM customers;
```

------------------------------------------------------------------------

## 3. CONVERT()

### Syntax

``` sql
CONVERT(expression, datatype)
```

### Example

``` sql
SELECT CONVERT('100', SIGNED);
```

### Table Example

``` sql
SELECT 
    orderNumber,
    CONVERT(orderNumber, CHAR) AS order_text
FROM orders;
```

✔ CAST is preferred (standard SQL)

------------------------------------------------------------------------

## 4. STR_TO_DATE()

### Syntax

``` sql
STR_TO_DATE(string, format)
```

### Format Specifiers

-   %Y → Year
-   %m → Month
-   %d → Day
-   %H → Hour
-   %i → Minute
-   %s → Second

### Example

``` sql
SELECT STR_TO_DATE('20-03-2026', '%d-%m-%Y');
```

### With Time

``` sql
SELECT STR_TO_DATE('20-03-2026 14:30:00', '%d-%m-%Y %H:%i:%s');
```

### Common Error

``` sql
STR_TO_DATE('2026-03-20', '%d-%m-%Y'); -- NULL
```

------------------------------------------------------------------------

## 5. DATE_FORMAT()

### Syntax

``` sql
DATE_FORMAT(date, format)
```

### Examples

``` sql
SELECT DATE_FORMAT(NOW(), '%d-%m-%Y');
SELECT DATE_FORMAT(NOW(), '%W, %M %d, %Y');
```

### classicmodels Example

``` sql
SELECT 
    orderNumber,
    DATE_FORMAT(orderDate, '%d-%m-%Y') AS formatted_date
FROM orders;
```

------------------------------------------------------------------------

## 6. String → Number

``` sql
SELECT CAST('2500' AS DECIMAL(10,2));
SELECT CAST('25ABC' AS SIGNED); -- Result: 25
```

------------------------------------------------------------------------

## 7. Number → String

``` sql
SELECT CONCAT('USD ', CAST(1000 AS CHAR));
```

### classicmodels Example

``` sql
SELECT 
    customerName,
    CONCAT('Credit Limit: ', CAST(creditLimit AS CHAR)) AS info
FROM customers;
```

------------------------------------------------------------------------

## 8. Combined Query

``` sql
SELECT 
    o.orderNumber,
    DATE_FORMAT(o.orderDate, '%d-%m-%Y') AS order_date,
    CONCAT('USD ', CAST(p.amount AS CHAR)) AS payment_amount
FROM orders o
JOIN payments p 
    ON o.customerNumber = p.customerNumber;
```

------------------------------------------------------------------------

## 9. Common Errors

### Wrong Format

``` sql
STR_TO_DATE('2026-03-20', '%d-%m-%Y');
```

### Silent Conversion

``` sql
SELECT 'ABC' + 10; -- Result: 10
```

------------------------------------------------------------------------

## 10. Exercises

### 🟢 Beginner

-   Convert '500' to number
-   Convert NOW() to DD-MM-YYYY
-   Convert 1000 to string

### 🟡 Intermediate

-   Format orderDate → March 20, 2026
-   Convert '01/15/2024' to DATE
-   Show creditLimit with USD

### 🔴 Advanced

-   Build report with formatted date and amount
-   Use JOIN with conversion
-   Detect invalid numeric strings

------------------------------------------------------------------------

## 📝 11. Summary

  Function      Purpose
  ------------- --------------------
  CAST          General conversion
  CONVERT       Alternative
  STR_TO_DATE   String → Date
  DATE_FORMAT   Date → String

------------------------------------------------------------------------
