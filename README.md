# SQL Practice Queries
This repository contains a collection of SQL queries ranging from basic to advanced levels, curated for developers who wish to strengthen their SQL skills. You are encouraged to review each query, attempt writing the solution independently, and then verify your approach with the provided answers.

## Queries

---

### Query 1

**Question:** Get all columns and data from a table named `departments`.

```sql
SELECT * FROM departments;
```

---

### Query 2

**Question:** Fetch only `name` and `email` of all users from the `users` table.

```sql
SELECT name, email FROM users;
```

---

### Query 3

**Question:** Get all orders from the `orders` table where the `status` is 'shipped' and the `total_amount` is greater than 1000.

```sql
SELECT * FROM orders WHERE status = 'shipped' AND total_amount > 1000;
```

---

### Query 4

**Question:** Fetch `name`, `email` from the `users` table where the `city` is 'Ahmedabad' or 'Surat'.

```sql
SELECT name, email FROM users WHERE city = 'Ahmedabad' OR city = 'Surat';
```

---

### Query 5

**Question:** Retrieve all employees with a `salary` between 40,000 and 80,000 (inclusive) from the `employees` table.

```sql
SELECT * FROM employees WHERE salary BETWEEN 40000 AND 80000;
```

---

### Query 6

**Question:** Get all data from the `products` table and sort the result by `price` in descending order.

```sql
SELECT * FROM products ORDER BY price DESC;
```

---

### Query 7

**Question:** Fetch all unique cities from the `customers` table.

```sql
SELECT DISTINCT city FROM customers;
```

---

### Query 8

**Question:** Retrieve the top 5 highest-paid employees from the `employees` table (use `salary` column).

```sql
SELECT * FROM employees ORDER BY salary DESC LIMIT 5;
```

---

### Query 9

**Question:** Get the total number of users from the `users` table.

```sql
SELECT COUNT(*) FROM users;
```

---

### Query 10

**Question:** Find the average salary of all employees in the `employees` table.

```sql
SELECT AVG(salary) FROM employees;
```

---

### Query 11

**Question:** Count how many orders have the status 'pending' in the `orders` table.

```sql
SELECT COUNT(*) FROM orders WHERE status = 'pending';
```

---

### Query 12

**Question:** Find the average salary of all employees in the employees table.

```sql
SELECT AVG(salary) FROM employees;
```

---

### Query 13

**Question:** Count how many orders have the status 'pending' in the orders table.

```sql
SELECT COUNT(*) FROM orders WHERE status = 'pending';
```

---

### Query 14

**Question:** List each city from the customers table and count how many customers belong to each city.

```sql
SELECT city, COUNT(*) AS customer_count FROM customers GROUP BY city;
```

---

### Query 15

**Question:** Get the average salary of employees grouped by department_id from the employees table.

```sql
SELECT department_id, AVG(salary) AS avg_salary FROM employees GROUP BY department_id;
```

---

### Query 16

**Question:** From the orders table, find statuses that have more than 10 orders.

```sql
SELECT status, COUNT(*) AS total_orders FROM orders GROUP BY status HAVING COUNT(*) > 10;
```

---

### Query 17

**Question:** Fetch all product names along with their category names using products and categories tables.

```sql
SELECT products.name AS product_name, categories.name AS category_name FROM products LEFT JOIN categories ON products.category_id = categories.id;
```

---

### Query 18

**Question:** Get the total number of orders placed by each user. Show user_id and the count, using the orders table.

```sql
SELECT user_id, COUNT(*) AS total_orders FROM orders GROUP BY user_id;
```

---

### Query 19

**Question:** List each product along with its category name, even if the product doesn’t have a category assigned.

```sql
SELECT products.name AS product_name, categories.name AS category_name FROM products LEFT JOIN categories ON products.category_id = categories.id;
```

---

### Query 20

**Question:** Get the names of users who have not placed any order.

```sql
SELECT name FROM users LEFT JOIN orders ON users.id = orders.user_id WHERE orders.user_id IS NULL;
```

---

### Query 21

**Question:** List all orders where the delivery_date is NULL.

```sql
SELECT * FROM orders WHERE delivery_date IS NULL;
```

---

### Query 22

**Question:** Get names of products that belong to categories named 'Electronics' or 'Grocery'.

```sql
SELECT products.name FROM products INNER JOIN categories ON products.category_id = categories.id WHERE categories.name IN ('Electronics', 'Grocery');
```

---

### Query 23

**Question:** From orders table, list statuses that have more than 5 orders.

```sql
SELECT status, COUNT(*) AS total_orders FROM orders GROUP BY status HAVING COUNT(*) > 5;
```

---

### Query 24

**Question:** List all users who have never placed an order.

```sql
SELECT * FROM users WHERE id NOT IN (SELECT user_id FROM orders WHERE user_id IS NOT NULL);
```

---

### Query 25

**Question:** Get names of products in categories containing 'Food'.

```sql
SELECT name FROM products WHERE category_id IN (SELECT id FROM categories WHERE name LIKE '%Food%');
```

---

### Query 26

**Question:** Get all orders, show 'Not Delivered' if delivery_date is NULL using COALESCE.

```sql
SELECT order_id, COALESCE(delivery_date, 'Not Delivered') AS delivery_status FROM orders;
```

---

### Query 27

**Question:** Find the second highest salary from employees.

```sql
SELECT salary FROM employees ORDER BY salary DESC LIMIT 1 OFFSET 1;
```

---

### Query 28

**Question:** Show order_id, total_amount, and a label 'order_type' as 'High', 'Medium', 'Low' based on amount.

```sql
SELECT order_id, total_amount,
  CASE
    WHEN total_amount > 1000 THEN 'HIGH'
    WHEN total_amount > 500 AND total_amount <= 1000 THEN 'MEDIUM'
    ELSE 'LOW'
  END AS order_type
FROM orders;
```

---

### Query 29

**Question:** Find users who placed more than 3 orders.

```sql
SELECT users.name, COUNT(*) AS order_count
FROM users
INNER JOIN orders ON users.id = orders.user_id
GROUP BY users.id, users.name
HAVING COUNT(*) > 3;
```

---

### Query 30

**Question:** List all products that do not belong to any category.

```sql
SELECT products.*
FROM products
LEFT JOIN categories ON products.category_id = categories.id
WHERE categories.id IS NULL;
```

---

### Query 31

**Question:** Get a combined list of all customer emails and vendor emails (from customers and vendors tables) without duplicates.

```sql
SELECT email FROM customers
UNION
SELECT email FROM vendors;
```

---

### Query 32

**Question:** Get the 3 most expensive products in each category.

```sql
SELECT * FROM (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY category_id ORDER BY price DESC) AS rank
  FROM products
) AS ranked_products
WHERE rank <= 3;
```

---

### Query 33

**Question:** List users whose phone_number is either NULL or an empty string.

```sql
SELECT * FROM users WHERE phone_number IS NULL OR phone_number = '';
```

---

### Query 34

**Question:** For each department, get the total number of employees and average salary.

```sql
SELECT department_id, COUNT(*) AS total_employees, AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;
```

---

### Query 35

**Question:** Find employees who have the same manager (use self-join).

```sql
SELECT e.employee_name AS employee, m.employee_name AS manager
FROM employees AS e
JOIN employees AS m ON e.manager_id = m.employee_id;
```

---

### Query 36

**Question:** List all users who have placed at least one order.

```sql
SELECT * 
FROM users u
WHERE EXISTS (
  SELECT 1 
  FROM orders o 
  WHERE o.user_id = u.id
);
```

---

### Query 37

**Question:** List products that are more expensive than all products in the 'Books' category.

```sql
SELECT * 
FROM products 
WHERE price > ALL (
  SELECT price 
  FROM products 
  WHERE category = 'BOOKS'
);
```

---

### Query 38

**Question:** Find categories where the average product price is more than ₹500.

```sql
SELECT c.*
FROM categories c
JOIN (
  SELECT category_id
  FROM products
  GROUP BY category_id
  HAVING AVG(price) > 500
) AS filtered
ON c.id = filtered.category_id;
```

---

### Query 39

**Question:** Find users with more than 5 orders and display their total spent.

```sql
SELECT u.id, u.name, SUM(o.total_amount) AS total_spent, COUNT(*) AS total_orders
FROM users u
JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.name
HAVING COUNT(*) > 5;
```

---

### Query 40

**Question:** Get the category name and count of products in each category (including categories with 0 products).

```sql
SELECT c.name, COUNT(p.id) AS product_count
FROM categories c
LEFT JOIN products p ON c.id = p.category_id
GROUP BY c.id, c.name;
```

---

### Query 41

**Question:** Show each product name and the average price of all products (as a separate column).

```sql
SELECT 
  name, 
  price,
  (SELECT AVG(price) FROM products) AS average_price
FROM products;
```

---

### Query 42

**Question:** Find users who have placed duplicate orders (same user_id and product_id).

```sql
SELECT u.name 
FROM users u
JOIN orders o ON u.id = o.user_id
GROUP BY o.user_id, o.product_id, u.name
HAVING COUNT(*) > 1;
```

---

### Query 43

**Question:** For each department, show department name, total employees, and number of employees with salary > ₹60,000.

```sql
SELECT 
  d.name AS department_name,
  COUNT(e.id) AS total_employees,
  COUNT(CASE WHEN e.salary > 60000 THEN 1 END) AS high_earners
FROM department d
JOIN employees e ON d.id = e.department_id
GROUP BY d.id, d.name;
```

---

### Query 44

**Question:** List all categories that have no products.

```sql
SELECT * 
FROM categories c
WHERE NOT EXISTS (
  SELECT 1 
  FROM products p 
  WHERE p.category_id = c.id
);
```

---

### Query 45

**Question:** List all products that belong to either 'Clothing', 'Footwear', or 'Accessories' categories.

```sql
SELECT * 
FROM products p
JOIN categories c ON p.category_id = c.id
WHERE c.name IN ('Clothing', 'Footwear', 'Accessories');
```

---

### Query 46

**Question:** List all products with price between ₹500 and ₹1500 (inclusive).

```sql
SELECT * FROM products WHERE price BETWEEN 500 AND 1500;
```

---

### Query 47

**Question:** Find all users who haven't provided an email (email is either NULL or empty).

```sql
SELECT * FROM users 
WHERE email IS NULL OR email = '';
```

---

### Query 48

**Question:** List each city and the number of users from that city, ordered by count descending.

```sql
SELECT city, COUNT(*) AS user_count
FROM users
GROUP BY city
ORDER BY user_count DESC;
```

---

### Query 49

**Question:** Fetch the top 3 highest paid employees.

```sql
SELECT * FROM employees ORDER BY salary DESC LIMIT 3;
```

---

### Query 50

**Question:** Find all users whose email ends with @gmail.com.

```sql
SELECT * FROM users WHERE email LIKE '%@gmail.com';
```

---

### Query 51

**Question:** List departments having more than 5 employees.

```sql
SELECT d.id, d.name, COUNT(e.id) AS total_employees
FROM departments d
JOIN employees e ON d.id = e.department_id
GROUP BY d.id, d.name
HAVING COUNT(e.id) > 5;
```

---

### Query 52

**Question:** Find the product(s) with the maximum price.

```sql
SELECT * FROM products WHERE price = (SELECT MAX(price) FROM products);
```

---

### Query 53

**Question:** List all orders placed in the last 30 days.

```sql
SELECT * FROM orders WHERE order_date >= CURDATE() - INTERVAL 30 DAY;
```

---

### Query 54

**Question:** List all users who have placed at least one order.

```sql
SELECT * FROM users 
WHERE EXISTS (
  SELECT 1 FROM orders WHERE orders.user_id = users.id
);
```

---

### Query 55

**Question:** Get a combined list of all customer and vendor emails (including duplicates).

```sql
SELECT email FROM customer 
UNION ALL 
SELECT email FROM vendor 
ORDER BY email;
```

---

### Query 56

**Question:** Fetch all employees who have a non-null manager_id.

```sql
SELECT * FROM employees WHERE manager_id IS NOT NULL;
```

---

### Query 57

**Question:** Find all products with a price greater than any product in the 'Stationery' category.

```sql
SELECT * FROM products 
WHERE price > ANY (
  SELECT price FROM products p
  JOIN categories c ON p.category_id = c.id
  WHERE c.name = 'Stationery'
);
```

---

### Query 58

**Question:** Get all users who have more than 1 order (without explicit GROUP BY).

```sql
SELECT * FROM users 
WHERE id IN (
  SELECT user_id FROM orders HAVING COUNT(*) > 1
);
```

---

### Query 59

**Question:** List all users who have never placed an order.

```sql
SELECT * FROM users 
WHERE id NOT IN (
  SELECT user_id FROM orders
);
```

---

### Query 60

**Question:** List employees whose salary is higher than the average salary of their department.

```sql
SELECT e.name, e.salary, e.department_id
FROM employees e
WHERE e.salary > (
  SELECT AVG(e2.salary)
  FROM employees e2
  WHERE e2.department_id = e.department_id
);
```

---

### Query 61

**Question:** Get a list of user emails that appear in both the customers and vendors tables.

```sql
SELECT email FROM customers
INTERSECT
SELECT email FROM vendors;
```

---

### Query 62

**Question:** List the average product price per category, but only for categories where the average price is above ₹1000.

```sql
SELECT category_id, avg_price 
FROM (
  SELECT category_id, AVG(price) AS avg_price 
  FROM products 
  GROUP BY category_id
) AS category_avg
WHERE avg_price > 1000;
```

---

### Query 63

**Question:** Fetch a combined list of all employees and their managers.

```sql
SELECT e.name AS employee, m.name AS manager
FROM employees e
FULL OUTER JOIN employees m ON e.manager_id = m.id;
```

---

### Query 64

**Question:** Count the number of unique cities from which users have placed orders.

```sql
SELECT COUNT(DISTINCT u.city)
FROM users u
JOIN orders o ON u.id = o.user_id;
```

---

### Query 65

**Question:** Find users who placed an order with the maximum total amount across all orders.

```sql
SELECT u.name, o.total_amount
FROM users u
JOIN orders o ON u.id = o.user_id
WHERE o.total_amount = (SELECT MAX(total_amount) FROM orders);
```

---

### Query 66

**Question:** Generate a combination of all users and all available user roles.

```sql
SELECT u.name AS user_name, r.role_name
FROM users u
CROSS JOIN roles r;
```

---

### Query 67

**Question:** List all users who are not vendors.

```sql
SELECT u.*
FROM users u
LEFT JOIN vendors v ON u.id = v.id
WHERE v.id IS NULL;
```

---

### Query 68

**Question:** Get the count of orders per user, separating them into 'shipped' and 'pending' using conditional aggregation.

```sql
SELECT 
  user_id,
  COUNT(CASE WHEN status = 'shipped' THEN 1 END) AS shipped_orders,
  COUNT(CASE WHEN status = 'pending' THEN 1 END) AS pending_orders
FROM orders
GROUP BY user_id;
```

---

### Query 69

**Question:** List all product names that belong to categories managed by employees in the 'Sales' department.

```sql
SELECT p.name 
FROM products p
JOIN categories c ON p.category_id = c.id
JOIN employees e ON c.manager_id = e.id
JOIN departments d ON e.department_id = d.id
WHERE d.name = 'Sales';
```

---

### Query 70

**Question:** List all users who have not placed any orders.

```sql
SELECT * 
FROM users u
WHERE NOT EXISTS (
  SELECT 1 
  FROM orders o 
  WHERE o.user_id = u.id
);
```

---

### Query 71

**Question:** Find departments with more than 3 employees and show the average salary in those departments.

```sql
SELECT d.name, AVG(e.salary) AS avg_salary
FROM departments d
JOIN employees e ON d.id = e.department_id
GROUP BY d.name
HAVING COUNT(e.id) > 3;
```

---

### Query 72

**Question:** Get the total order amount grouped by user and order status, ordered by user ID and status.

```sql
SELECT 
  orders.user_id, 
  orders.status, 
  SUM(orders.amount) AS order_amount
FROM orders
JOIN users ON orders.user_id = users.id
GROUP BY orders.user_id, orders.status
ORDER BY orders.user_id, orders.status;
```

--- 
