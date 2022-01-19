# Shopify Intern Challenge

## Question 1 

Given some sample data, write a program to answer the following: [click here to access the required data set.](https://docs.google.com/spreadsheets/d/16i38oonuX1y1g7C_UAmiK9GkY7cS-64DfiDMNiR41LM/edit#gid=0) On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

A. Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 
  
  - The issue with the calculation including the outliers within the calculation.

B. What metric would you report for this dataset?

  - The same metric can be used after cleaning the data.

C. What is its value?

  - Because of the outliers, the average value is highly skewed to 3,145.13 dollars. Without the outliers, the mistakenly priced item at 25,725.00 dollars and the extremely high order count of 2,000 items per order with a total order value of 704,000.00 dollars per, the average order value is 792.34 dollars.

## Question 2 

For this question you’ll need to use SQL. [Follow this link](https://www.w3schools.com/SQL/TRYSQL.ASP?FILENAME=TRYSQL_SELECT_ALL) to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

A. How many orders were shipped by Speedy Express in total?

  - SELECT COUNT (OrderID)
    
    FROM Orders
    
    WHERE ShipperID = 1;

  - Speedy Express shipped 54 orders total

B. What is the last name of the employee with the most orders?

  - SELECT Employees.LastName, COUNT(Orders.EmployeeID) AS NumberOfOrders
    
    FROM Orders
    
    LEFT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
    
    GROUP BY LastName
    
    ORDER BY NumberOfOrders DESC;
    
  - The last name of the employee with the most orders is "Peacock"

C. What product was ordered the most by customers in Germany?

  - CREATE TABLE GermanCustomers AS
    
    SELECT Customers.CustomerName, Orders.OrderID
    
    FROM Customers
    
    INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID 
    
    WHERE Country='Germany';
    
    CREATE TABLE GermanOrders AS
    
    SELECT * FROM OrderDetails

    INNER JOIN GermanCustomers ON GermanCustomers.OrderID = OrderDetails.OrderID;
    
    CREATE TABLE GermanSum AS
    
    SELECT ProductID, SUM(Quantity) AS SUM FROM GermanOrders
    
    GROUP BY ProductID;
    
    SELECT ProductName, GermanSum.SUM FROM Products
   
    INNER JOIN GermanSum ON GermanSum.ProductID = Products.ProductID
    
    ORDER BY (SUM) DESC;
    
   - The product ordered by the most customers in Germany is Boston Crab Meat
