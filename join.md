# SQL JOINs

## Lesson Objectives
By the end of this lesson, students will be able to:
- Understand how tables relate in a real database
- Use different JOIN types correctly
- Predict query results before execution
- Write JOIN queries using real business data

---

## 1. INNER JOIN

### Concept
Returns **only matching rows** from both tables.

```Show records that exist in **both tables**.```

### Example
- Customer with orders → shown
- Customer without orders → NOT shown

### SQL Example
```sql
SELECT 
    customers.customerNumber,
    customers.customerName,
    orders.orderNumber,
    orders.orderDate
FROM customers
INNER JOIN orders
ON customers.customerNumber = orders.customerNumber;
```

---

## 2. LEFT JOIN

### Concept
Returns **all rows from the LEFT table**, even if there is **no match** in the RIGHT table.

### Example
- Customer with orders → shown
- Customer without orders → shown as NULL

### SQL Example
```sql
SELECT 
    customers.customerName,
    orders.orderNumber
FROM customers
LEFT JOIN orders
ON customers.customerNumber = orders.customerNumber;
```

---

## 3. RIGHT JOIN

### Concept
Returns **all rows from the RIGHT table**, even if there is **no match** in the LEFT table.

### Example
- Order with customer → shown
- Order without customer → shown as NULL

### SQL Example
```sql
SELECT 
    customers.customerName,
    orders.orderNumber
FROM customers
RIGHT JOIN orders
ON customers.customerNumber = orders.customerNumber;
```

---

## 4. SELF JOIN

### Concept
A table joins **with itself** to compare rows.

### Example
- Employees and their managers are in the same table

### 🧪 SQL Example
```sql
SELECT 
    e.employeeNumber,
    e.firstName AS employeeName,
    m.firstName AS managerName
FROM employees e
LEFT JOIN employees m
ON e.reportsTo = m.employeeNumber;
```

---

## 5. CROSS JOIN

### Concept
Returns **every possible combination** of rows from two tables.

### Example
- 3 products × 2 offices = 6 rows

### SQL Example
```sql
SELECT 
    products.productName,
    offices.city
FROM products
CROSS JOIN offices;
```

````
1.បង្ហាញបញ្ជីឈ្មោះអតិថិជនទាំងអស់ ដែលធ្លាប់បានបញ្ជាទិញទំនិញយ៉ាងតិចមួយដង។
2.បង្ហាញឈ្មោះអតិថិជន លេខវិក្កយបត្រ និងកាលបរិច្ឆេទបញ្ជាទិញ សម្រាប់ការបញ្ជាទិញដែលមានស្រាប់ទាំងអស់។
3.បង្ហាញបញ្ជីឈ្មោះអតិថិជនទាំងអស់ និងលេខវិក្កយបត្ររបស់ពួកគេ (រួមបញ្ចូលទាំងអតិថិជនដែលមិនធ្លាប់បញ្ជាទិញផងដែរ)។
4.ស្វែងរកអតិថិជនដែល មិនធ្លាប់បានបញ្ជាទិញទំនិញសោះ។
5.បង្ហាញបញ្ជីការបញ្ជាទិញទាំងអស់ និងឈ្មោះអតិថិជន រួមបញ្ចូលទាំងការបញ្ជាទិញដែលមិនមានព័ត៌មានអតិថិជន។
6.បង្ហាញបញ្ជីបុគ្គលិក និងអ្នកគ្រប់គ្រង (Manager) របស់ពួកគេម្នាក់ៗ។
7.ស្វែងរកបុគ្គលិកដែលមិនមានអ្នកគ្រប់គ្រង។
8.បង្ហាញរាល់ការបញ្ចូលគ្នាដែលស្របទៅបានទាំងអស់ (Possible combinations) រវាងផលិតផល និងការិយាល័យ។
9.រាប់ចំនួនជួរ (Rows) សរុបដែលបង្កើតឡើងដោយ CROSS JOIN រវាងផលិតផល និងការិយាល័យ។
10.បង្ហាញឈ្មោះអតិថិជន លេខវិក្កយបត្រ និងឈ្មោះផលិតផល សម្រាប់ការបញ្ជាទិញទាំងអស់។
11.រកចំនួនសរុបនៃការបញ្ជាទិញដែលកាន់កាប់ដោយបុគ្គលិកផ្នែកលក់ (Sales rep) ម្នាក់ៗ។
````
