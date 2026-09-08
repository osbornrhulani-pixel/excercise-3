--- Step 1: creating catalog/ database
CREATE CATALOG IF NOT EXISTS exercise;
---step 2: creating a schema
CREATE SCHEMA IF NOT EXISTS exercise.case;
--- step 3: creating a table
CREATE TABLE IF NOT EXISTS exercise.case.products (
    product_id INT,
    product_name STRING, 
    price INT);
--- step 4: inserting data into table
INSERT INTO exercise.case.products VALUES 
(1, 'Laptop', 1200.00), 
(2, 'Phone', 800.00),
(3, 'Keyboard', 45.00),
(4, 'Monitor', 300.00),
(5, 'Mouse', 25.00);
--- step 5: querying the table
SELECT * FROM exercise.case.products;
--- Question 1: Classify each product by price into three teirs 
SELECT product_name,
     price,
     CASE 
        WHEN price > 1000 THEN 'Expensive'
        WHEN price BETWEEN 100 AND 1000 THEN 'Mid-range'
        WHEN price < 100 THEN 'Budget'
        END AS price_category
FROM exercise.case.products;

---- step 6: creating second table
CREATE TABLE IF NOT EXISTS exercise.case.orders (
    order_id INT,
    customer_name STRING,
    amount INT);
--- step 7: inserting data into table
INSERT INTO exercise.case.orders VALUES 
(1, 'Alice', 150.00),
(2, 'Bob', 560.00),
(3, 'Charlie', 999.99),
(4, 'Diana', 45.50),
(5, 'Ethan', 1200.00);
--- step 8: querying the table
SELECT * FROM exercise.case.orders;
--- Question 2: Label each order by its value into three categories highe value, mediun value and low value
SELECT customer_name,
     amount,
     CASE 
        WHEN amount >= 1000 THEN 'High Value'
        WHEN amount BETWEEN 500 AND 999.99 THEN 'Medium Value'
        WHEN amount < 500 THEN 'Low Value'
        END AS order_value_category
FROM exercise.case.orders;
--- step 9: creating third table
CREATE TABLE IF NOT EXISTS exercise.case.employees (
    emp_id INT,
    emp_name STRING,
    department STRING,
    salary INT);
--- step 10: inserting values
INSERT INTO exercise.case.employees VALUES 
(1, 'John', 'IT', 85000),
(2, 'Sara', 'HR', 60000),
(3, 'Mark', 'IT', 75000),
(4, 'Lucy', 'Finance', 95000),
(5, 'Tom', 'HR', 55000);
--- query the table
SELECT * FROM exercise.case.employees;
--- Question 3: categorise each employee's position level using both department and salary
SELECT emp_name,
     department,
     salary,
     CASE 
        WHEN department = 'IT' AND salary > 80000 THEN 'Senior IT'
        WHEN department = 'HR' AND salary > 55000 THEN 'Experienced HR'
        ELSE 'Staff'
        END AS employee_level
FROM exercise.case.employees;
--- step 11 creating fourth table 
CREATE TABLE IF NOT EXISTS exercise.case.students (
    student_id INT,
    student_name STRING,
    score INT);
--- step 12 inserting values
INSERT INTO exercise.case.students VALUES 
(1, 'Anna', 92),
(2, 'Ben', 76),
(3, 'Cara', 59),
(4, 'David', 83),
(5, 'Ella', 68);
--- query the table
SELECT * FROM exercise.case.students;
--- question 4: assign each student a letter grade based on their score
SELECT student_name,
     score,
     CASE 
        WHEN score >= 90 THEN 'A'
        WHEN score BETWEEN 80 AND 89 THEN 'B'
        WHEN score BETWEEN 70 AND 79 THEN 'C'
        WHEN score BETWEEN 60 AND 69 THEN 'D'
        WHEN score < 60 THEN 'F'
        END AS grade
    FROM exercise.case.students;
    --- step 12: creating the fifth table 
    CREATE TABLE IF NOT EXISTS exercise.case.deliveries (
    delivery_id INT,
    delivery_time_minutes INT);
--- step 13: inserting values
INSERT INTO exercise.case.deliveries VALUES 
(1, 45),
(2, 80),
(3, 30),
(4, 65),
(5, 100);
--- query the table
SELECT * FROM exercise.case.deliveries;
--- question 5: label delivery performance based on the time taken 
SELECT delivery_id,
     delivery_time_minutes,
     CASE 
        WHEN delivery_time_minutes <= 30 THEN 'Fast'
        WHEN delivery_time_minutes BETWEEN 31 AND 60 THEN 'On Time'
        WHEN delivery_time_minutes > 60 THEN 'Late'
        END AS performance
FROM exercise.case.deliveries;
--- step 14: creating the sixth table 
CREATE TABLE IF NOT EXISTS exercise.case.tickets (
    ticket_id INT,
    issue_type STRING,
    priority INT);
--- step 15: inserting values
INSERT INTO exercise.case.tickets VALUES 
(1, 'Login issue', 1),
(2, 'Sever down', 3),
(3, 'Slow system', 2),
(4, 'Email error', 2),
(5, 'Password reset', 1);
--- query the table
SELECT * FROM exercise.case.tickets;
--- question 6: convert numeric priority into a readable label
SELECT issue_type,
     priority,
     CASE 
        WHEN priority = 3 THEN 'High'
        WHEN priority = 2 THEN 'Medium'
        WHEN priority = 1 THEN 'Low'
        END AS priority_label
FROM exercise.case.tickets;
--- step 16: creating the seventh table 
CREATE TABLE IF NOT EXISTS exercise.case.attendance (
    student_id INT,
    days_present INT,
    total_days INT);
--- step 17: inserting values into the table
INSERT INTO exercise.case.attendance VALUES 
(1, 45, 50),
(2, 30, 50),
(3, 48, 50),
(4, 25, 50),
(5, 50, 50);
--- query the table
SELECT * FROM exercise.case.attendance;
--- Question 7: Calculate attendance percentage and classify the result
SELECT student_id,
(days_present/total_days)*100 AS attendance_percentage,
      CASE 
          WHEN (days_present/total_days)*100 >= 90 THEN 'Excellent'
          WHEN (days_present/total_days)*100 BETWEEN 75 AND 89 THEN 'Good'
          WHEN (days_present/total_days)*100 < 75 THEN 'Needs Improvement'
          END AS attendance_status
       FROM exercise.case.attendance;   
          

--- step 18: creating the eighth table 
CREATE TABLE IF NOT EXISTS exercise.case.product_inventory (
    product_id INT,
    stock_qty INT);
--- step 19: inserting values into the table
INSERT INTO exercise.case.product_inventory VALUES 
(1, 5),
(2, 0),
(3, 25),
(4, 10),
(5, 3);
--- query table
SELECT * FROM exercise.case.product_inventory;
--- question 8: classify products based on their stock levels
SELECT product_id,
       stock_qty,
   CASE
       WHEN stock_qty = 0 THEN 'Out of Stock'
       WHEN stock_qty BETWEEN 1 AND 5 THEN 'Low Stock'
       WHEN stock_qty > 5 THEN 'In Stock'
       END AS stock_status
   FROM exercise.case.product_inventory;    
--- step 20: creating the ninth table 
CREATE TABLE IF NOT EXISTS exercise.case.classes (
    class_id INT,
    subject STRING,
    enrolled_students INT);
--- step 21: inserting values into the table
INSERT INTO exercise.case.classes VALUES 
(1, 'Math', 30),
(2, 'English', 25),
(3, 'Science', 15),
(4, 'Art', 5),
(5, 'History', 20);
--- query the table
SELECT * FROM exercise.case.classes;
--- question 9: classify each class based on the number of enrolled students
SELECT subject,
       enrolled_students,
       CASE
           WHEN enrolled_students >= 25 THEN 'Large'
           WHEN enrolled_students BETWEEN 10 AND 24 THEN 'Medium'
           WHEN enrolled_students < 10 THEN 'Small'
           END AS class_size_category
   FROM exercise.case.classes;        
--- step 22: creating the tenth table 
CREATE TABLE IF NOT EXISTS exercise.case.payments (
    payment_id INT,
    amount INT,
    payment_method STRING);    
--- step 23: inserting values into the table
INSERT INTO exercise.case.payments VALUES 
(1, 50.00, 'Card'),
(2, 200.00, 'Cash'),
(3, 150, 'Card'),
(4, 75.00, 'PayPal'),
(5, 300, 'Cash');
--- query the table
SELECT * FROM exercise.case.payments;
--- question 10: apply a discount flag based on the payment method
SELECT *,
      CASE 
           WHEN payment_method = 'Cash' AND amount >= 200 THEN 'Eligible for Discount'
           ELSE 'Not Eligible'
            END AS discount_eligibility
   FROM exercise.case.payments;
