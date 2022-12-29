# SQL Queries

$$\color{purple}{SQL \ Queries}$$

:link:[Home](all-file-links.md)     


<a name="top"></a>
 [Go To Bottom](#bottom)
 
 
# Topics

   [Go To Top](#top)
   
   [SQL Basic Queries](#sql_basic_queries) 
   
   [SQL Advanced Queries](#sql_advanced_queries)    
    
   [Top 14 Frequently asked SQL Query Interview Questions](#sql_interviews_questions_14)

   [Top 40 SQL Query Interview Questions and Answers for Practice](#sql_interviews_questions_40)

   [30 SQL Interviews Questions](#sql_interviews_questions_30)

   [Top 14 Frequently asked SQL Query Interview Questions](#more_examples_on_highest_salarary)
  
    




[Go To Top](#top)
<a name="sql_basic_queries"></a>
 # SQL Basic Queries
 
 Below is a selection from the "Customers" table:
 
CustomerID 	CustomerName 	                      ContactName 	       Address 	                      City 	     PostalCode 	  Country
1	          Alfreds Futterkiste 	               Maria Anders 	      Obere Str. 57 	                Berlin 	    12209 	      Germany 
2          	Ana Trujillo Emparedados y helados 	Ana Trujillo 	      Avda. de la Constitución 2222 	México D.F. 05021 	      Mexico
3 	         Antonio Moreno Taquería 	           Antonio Moreno      Mataderos 2312 	               México D.F. 05023   	    Mexico
4 	         Around the Horn 	                   Thomas Hardy 	      120 Hanover Sq. 	              London 	    WA1 1DP 	    UK
5 	         Berglunds snabbköp 	                Christina Berglund 	Berguvsvägen 8 	               Luleå 	     S-958 22 	   Sweden




ProductID 	ProductName 	SupplierID 	CategoryID 	Unit 	Price
1 	Chais 	1 	1 	10 boxes x 20 bags 	18
2 	Chang 	1 	1 	24 - 12 oz bottles 	19
3 	Aniseed Syrup 	1 	2 	12 - 550 ml bottles 	10
4 	Chef Anton's Cajun Seasoning 	2 	2 	48 - 6 oz jars 	22
5 	Chef Anton's Gumbo Mix 	2 	2 	36 boxes 	21.35


OrderDetailID 	OrderID 	ProductID 	Quantity
1 	10248 	11 	12
2 	10248 	42 	10
3 	10248 	72 	5
4 	10249 	14 	9
5 	10249 	51 	40


CustomerID	CustomerName	ContactName	Address	City	PostalCode	Country
1	Alfreds Futterkiste	Maria Anders	Obere Str. 57	Berlin	12209	Germany
2	Ana Trujillo Emparedados y helados	Ana Trujillo	Avda. de la Constitución 2222	México D.F.	05021	Mexico
3	Antonio Moreno Taquería	Antonio Moreno	Mataderos 2312	México D.F.	05023	Mexico
4	Around the Horn	Thomas Hardy	120 Hanover Sq.	London	WA1 1DP	UK
5	Berglunds snabbköp	Christina Berglund	Berguvsvägen 8	Luleå	S-958 22	Sweden
6	Blauer See Delikatessen	Hanna Moos	Forsterstr. 57	Mannheim	68306	Germany
7	Blondel père et fils	Frédérique Citeaux	24, place Kléber	Strasbourg	67000	France


Sample Table:

Below is a selection from the "Orders" table in the Northwind sample database:
OrderID 	CustomerID 	EmployeeID 	OrderDate 	ShipperID
10248 	90 	5 	7/4/1996 	3
10249 	81 	6 	7/5/1996 	1
10250 	34 	4 	7/8/1996 	2
10251 	84 	3 	7/9/1996 	1
10252 	76 	4 	7/10/1996 	2





 #Some of The Most Important SQL Commands:

    SELECT - extracts data from a database
    UPDATE - updates data in a database
    DELETE - deletes data from a database
    INSERT INTO - inserts new data into a database
    CREATE DATABASE - creates a new database
    ALTER DATABASE - modifies a database
    CREATE TABLE - creates a new table
    ALTER TABLE - modifies a table
    DROP TABLE - deletes a table
    CREATE INDEX - creates an index (search key)
    DROP INDEX - deletes an index


SQL SELECT Statement:

    SELECT * FROM table_name;  
    
The following SQL statement selects all the records in the "Customers" table:

    SELECT * FROM Customers;


    SELECT column1, column2, ...
    FROM table_name; 

   
    SELECT CustomerName, City FROM Customers;



SQL SELECT DISTINCT Statement:

    SELECT DISTINCT column1, column2, ...
    FROM table_name; 



SELECT Example Without DISTINCT:

    SELECT Country FROM Customers;
    
    SELECT DISTINCT Country FROM Customers;
    
    SELECT COUNT(DISTINCT Country) FROM Customers;


    SELECT Count(*) AS DistinctCountries
    FROM (SELECT DISTINCT Country FROM Customers);


SQL WHERE Clause:


    SELECT column1, column2, ...
    FROM table_name
    WHERE condition; 



    SELECT * FROM Customers
    WHERE Country='Mexico'; 


SELECT * FROM Customers
WHERE CustomerID=1; 



SQL AND, OR and NOT Operators:


AND Syntax:

    SELECT column1, column2, ...
    FROM table_name
    WHERE condition1 AND condition2 AND condition3 ...; 

OR Syntax:

    SELECT column1, column2, ...
    FROM table_name
    WHERE condition1 OR condition2 OR condition3 ...;

NOT Syntax:

    SELECT column1, column2, ...
    FROM table_name
    WHERE NOT condition; 




SELECT * FROM Customers
WHERE Country='Germany' AND City='Berlin';


SELECT * FROM Customers
WHERE City='Berlin' OR City='München';


SELECT * FROM Customers
WHERE Country='Germany' OR Country='Spain';


SELECT * FROM Customers
WHERE NOT Country='Germany';


SELECT * FROM Customers
WHERE Country='Germany' AND (City='Berlin' OR City='München'); 


SELECT * FROM Customers
WHERE NOT Country='Germany' AND NOT Country='USA'; 






SQL ORDER BY Keyword:


ORDER BY Syntax
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC; 


SELECT * FROM Customers
ORDER BY Country;



SELECT * FROM Customers
ORDER BY Country DESC; 


    SELECT * FROM Customers
    ORDER BY Country, CustomerName; 


    SELECT * FROM Customers
    ORDER BY Country ASC, CustomerName DESC; 



SQL INSERT INTO Statement:


INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...); 



INSERT INTO table_name
VALUES (value1, value2, value3, ...); 


INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');


INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');


SQL NULL Values:


IS NULL Syntax:

    SELECT column_names
    FROM table_name
    WHERE column_name IS NULL;

IS NOT NULL Syntax:

    SELECT column_names
    FROM table_name
    WHERE column_name IS NOT NULL; 


    SELECT CustomerName, ContactName, Address
    FROM Customers
    WHERE Address IS NULL;


    SELECT CustomerName, ContactName, Address
    FROM Customers
    WHERE Address IS NOT NULL;



SQL UPDATE Statement:



    UPDATE Syntax
    UPDATE table_name
    SET column1 = value1, column2 = value2, ...
    WHERE condition; 


    UPDATE Customers
    SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
    WHERE CustomerID = 1;


     UPDATE Customers
     SET ContactName='Juan'
     WHERE Country='Mexico';


     UPDATE Customers
     SET ContactName='Juan';


SQL DELETE Statement:


      DELETE FROM table_name WHERE condition;
    
      DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';

      DELETE FROM table_name;

      DELETE FROM Customers;



SQL TOP, LIMIT, FETCH FIRST or ROWNUM Clause:



SQL Server / MS Access Syntax:

     SELECT TOP number|percent column_name(s)
     FROM table_name
     WHERE condition;

MySQL Syntax:

     SELECT column_name(s)
     FROM table_name
     WHERE condition
     LIMIT number;

Oracle 12 Syntax:

     SELECT column_name(s)
     FROM table_name
     ORDER BY column_name(s)
     FETCH FIRST number ROWS ONLY;

Older Oracle Syntax:

     SELECT column_name(s)
     FROM table_name
     WHERE ROWNUM <= number;

Older Oracle Syntax (with ORDER BY):

     SELECT *
     FROM (SELECT column_name(s) FROM table_name ORDER BY column_name(s))
     WHERE ROWNUM <= number; 





SQL TOP, LIMIT and FETCH FIRST Examples:


SELECT TOP 3 * FROM Customers;

SELECT * FROM Customers
LIMIT 3; 


SELECT * FROM Customers
FETCH FIRST 3 ROWS ONLY; 



SELECT TOP 50 PERCENT * FROM Customers;


SELECT * FROM Customers
FETCH FIRST 50 PERCENT ROWS ONLY;



SELECT TOP 3 * FROM Customers
WHERE Country='Germany';


SELECT * FROM Customers
WHERE Country='Germany'
LIMIT 3; 



    SELECT * FROM Customers
    WHERE Country='Germany'
    FETCH FIRST 3 ROWS ONLY;



The SQL MIN() and MAX() Functions:


MIN() Syntax: 

    SELECT MIN(column_name)
    FROM table_name
    WHERE condition;

MAX() Syntax: 

    SELECT MAX(column_name)
    FROM table_name
    WHERE condition; 


    SELECT MIN(Price) AS SmallestPrice
    FROM Products;


    SELECT MAX(Price) AS LargestPrice
    FROM Products; 





SQL COUNT(), AVG() and SUM() Functions:




COUNT() Syntax:

    SELECT COUNT(column_name)
    FROM table_name
    WHERE condition; 

AVG() Syntax:

    SELECT AVG(column_name)
    FROM table_name
    WHERE condition; 

SUM() Syntax:

    SELECT SUM(column_name)
    FROM table_name
    WHERE condition; 

COUNT() :

SELECT COUNT(ProductID)
FROM Products;

AVG() : 

SELECT AVG(Price)
FROM Products;


SUM(): 

SELECT SUM(Quantity)
FROM OrderDetails; 



SQL LIKE Operator: 

LIKE Syntax
SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern; 


SQL LIKE: 

SELECT * FROM Customers
WHERE CustomerName LIKE 'a%'; 

SELECT * FROM Customers
WHERE CustomerName LIKE '%a'; 


SELECT * FROM Customers
WHERE CustomerName LIKE '%or%';


    SELECT * FROM Customers
    WHERE CustomerName LIKE '_r%';


    SELECT * FROM Customers
    WHERE CustomerName LIKE 'a__%'; 


    SELECT * FROM Customers
    WHERE ContactName LIKE 'a%o'; 


    SELECT * FROM Customers
    WHERE CustomerName NOT LIKE 'a%';



SQL Wildcard Characters: 


Using the % Wildcard


    SELECT * FROM Customers
    WHERE City LIKE 'ber%'; 


SELECT * FROM Customers
WHERE City LIKE '%es%';


SELECT * FROM Customers
WHERE City LIKE '_ondon';

SELECT * FROM Customers
WHERE City LIKE 'L_n_on';


SELECT * FROM Customers
WHERE City LIKE '[bsp]%';


SELECT * FROM Customers
WHERE City LIKE '[a-c]%';


    SELECT * FROM Customers
    WHERE City LIKE '[!bsp]%'; 

    SELECT * FROM Customers
    WHERE City NOT LIKE '[bsp]%'; 




SQL IN Operator: 


    SELECT column_name(s)
    FROM table_name
    WHERE column_name IN (value1, value2, ...); 


or:

    SELECT column_name(s)
    FROM table_name
    WHERE column_name IN (SELECT STATEMENT); 


SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');

SELECT * FROM Customers
WHERE Country NOT IN ('Germany', 'France', 'UK');


SELECT * FROM Customers
WHERE Country IN (SELECT Country FROM Suppliers);



SQL BETWEEN Operator: 



SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2; 

SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;


SELECT * FROM Products
WHERE Price NOT BETWEEN 10 AND 20;

SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20
AND CategoryID NOT IN (1,2,3);

SELECT * FROM Products
WHERE ProductName BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
ORDER BY ProductName;

SELECT * FROM Products
WHERE ProductName BETWEEN "Carnarvon Tigers" AND "Chef Anton's Cajun Seasoning"
ORDER BY ProductName;

    SELECT * FROM Products
    WHERE ProductName NOT BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
    ORDER BY ProductName;


    SELECT * FROM Orders
    WHERE OrderDate BETWEEN #07/01/1996# AND #07/31/1996#;

OR:

    SELECT * FROM Orders
    WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';


SQL Aliases: 

Alias Column Syntax:

    SELECT column_name AS alias_name
    FROM table_name;

Alias Table Syntax:

    SELECT column_name(s)
    FROM table_name AS alias_name; 


Alias for Columns: 

SELECT CustomerID AS ID, CustomerName AS Customer
FROM Customers; 

SELECT CustomerName AS Customer, ContactName AS [Contact Person]
FROM Customers;

SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address
FROM Customers; 

SELECT CustomerName, CONCAT(Address,', ',PostalCode,', ',City,', ',Country) AS Address
FROM Customers; 

SELECT CustomerName, (Address || ', ' || PostalCode || ' ' || City || ', ' || Country) AS Address
FROM Customers; 


SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerName='Around the Horn' AND c.CustomerID=o.CustomerID;


SELECT Orders.OrderID, Orders.OrderDate, Customers.CustomerName
FROM Customers, Orders
WHERE Customers.CustomerName='Around the Horn' AND Customers.CustomerID=Orders.CustomerID;



SQL Joins: 


OrderID 	CustomerID 	OrderDate
10308 	2 	1996-09-18
10309 	37 	1996-09-19
10310 	77 	1996-09-20

CustomerID 	CustomerName 	ContactName 	Country
1 	Alfreds Futterkiste 	Maria Anders 	Germany
2 	Ana Trujillo Emparedados y helados 	Ana Trujillo 	Mexico
3 	Antonio Moreno Taquería 	Antonio Moreno 	Mexico


SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;


and it will produce something like this:

OrderID 	CustomerName 	OrderDate
10308 	Ana Trujillo Emparedados y helados 	9/18/1996
10365 	Antonio Moreno Taquería 	11/27/1996
10383 	Around the Horn 	12/16/1996
10355 	Around the Horn 	11/15/1996
10278 	Berglunds snabbköp 	8/12/1996



Different Types of SQL JOINs: 

Here are the different types of the JOINs in SQL:

    (INNER) JOIN: Returns records that have matching values in both tables
    LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table
    RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table
    FULL (OUTER) JOIN: Returns all records when there is a match in either left or right table



SQL INNER JOIN Keyword: 


INNER JOIN Syntax
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;


OrderID 	CustomerID 	EmployeeID 	OrderDate 	ShipperID
10308 	2 	7 	1996-09-18 	3
10309 	37 	3 	1996-09-19 	1
10310 	77 	8 	1996-09-20 	2


CustomerID 	CustomerName 	ContactName 	Address 	City 	PostalCode 	Country

1	Alfreds Futterkiste 	Maria Anders 	Obere Str. 57 	Berlin 	12209 	Germany
2 Ana Trujillo Emparedados y helados 	Ana Trujillo 	Avda. de la Constitución 2222 	México D.F. 	05021 	Mexico
3 Antonio Moreno Taquería 	Antonio Moreno 	Mataderos 2312 	México D.F. 	05023 	Mexico



Example:

    SELECT Orders.OrderID, Customers.CustomerName
    FROM Orders
    INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID; 


JOIN Three Tables: 

Example:

    SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
    FROM ((Orders
    INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
    INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID); 



SQL LEFT JOIN Keyword:

LEFT JOIN Syntax:

    SELECT column_name(s)
    FROM table1
    LEFT JOIN table2
    ON table1.column_name = table2.column_name;


CustomerID 	CustomerName 	ContactName 	Address 	City 	PostalCode 	Country
1

	Alfreds Futterkiste 	Maria Anders 	Obere Str. 57 	Berlin 	12209 	Germany
2 	Ana Trujillo Emparedados y helados 	Ana Trujillo 	Avda. de la Constitución 2222 	México D.F. 	05021 	Mexico
3 	Antonio Moreno Taquería 	Antonio Moreno 	Mataderos 2312 	México D.F. 	05023 	Mexico


And a selection from the "Orders" table:
OrderID 	CustomerID 	EmployeeID 	OrderDate 	ShipperID
10308 	2 	7 	1996-09-18 	3
10309 	37 	3 	1996-09-19 	1
10310 	77 	8 	1996-09-20 	2


SQL LEFT JOIN Example:

The following SQL statement will select all customers, and any orders they might have:

Example:

    SELECT Customers.CustomerName, Orders.OrderID
    FROM Customers
    LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
    ORDER BY Customers.CustomerName;


SQL RIGHT JOIN Keyword: 

RIGHT JOIN Syntax:

    SELECT column_name(s)
    FROM table1
    RIGHT JOIN table2
    ON table1.column_name = table2.column_name;


OrderID 	CustomerID 	EmployeeID 	OrderDate 	ShipperID
10308 	2 	7 	1996-09-18 	3
10309 	37 	3 	1996-09-19 	1
10310 	77 	8 	1996-09-20 	2

And a selection from the "Employees" table:
EmployeeID 	LastName 	FirstName 	BirthDate 	Photo
1 	Davolio 	Nancy 	12/8/1968 	EmpID1.pic
2 	Fuller 	Andrew 	2/19/1952 	EmpID2.pic
3 	Leverling 	Janet 	8/30/1963 	EmpID3.pic


SQL RIGHT JOIN Example:

SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID; 




SQL FULL OUTER JOIN Keyword: 

FULL OUTER JOIN Syntax:

SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name
WHERE condition; 


CustomerID 	CustomerName 	ContactName 	Address 	City 	PostalCode 	Country
1	Alfreds Futterkiste 	Maria Anders 	Obere Str. 57 	Berlin 	12209 	Germany
2 	Ana Trujillo Emparedados y helados 	Ana Trujillo 	Avda. de la Constitución 2222 	México D.F. 	05021 	Mexico
3 	Antonio Moreno Taquería 	Antonio Moreno 	Mataderos 2312 	México D.F. 	05023 	Mexico


OrderID 	CustomerID 	EmployeeID 	OrderDate 	ShipperID
10308 	2 	7 	1996-09-18 	3
10309 	37 	3 	1996-09-19 	1
10310 	77 	8 	1996-09-20 	2


SQL FULL OUTER JOIN Example: 

SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL OUTER JOIN Orders ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName;


SQL Self Join: 

A self join is a regular join, but the table is joined with itself.

Self Join Syntax
SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;


CustomerID 	CustomerName 	ContactName 	Address 	City 	PostalCode 	Country
1	Alfreds Futterkiste 	Maria Anders 	Obere Str. 57 	Berlin 	12209 	Germany
2 	Ana Trujillo Emparedados y helados 	Ana Trujillo 	Avda. de la Constitución 2222 	México D.F. 	05021 	Mexico
3 	Antonio Moreno Taquería 	Antonio Moreno 	Mataderos 2312 	México D.F.



SQL Self Join Example:

The following SQL statement matches customers that are from the same city:

	SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City
	FROM Customers A, Customers B
	WHERE A.CustomerID <> B.CustomerID
	AND A.City = B.City
	ORDER BY A.City;


SQL UNION Operator: 

UNION Syntax:

SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;


UNION ALL Syntax:

SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2; 

CustomerID 	CustomerName 	ContactName 	Address 	City 	PostalCode 	Country
1	Alfreds Futterkiste 	Maria Anders 	Obere Str. 57 	Berlin 	12209 	Germany
2 	Ana Trujillo Emparedados y helados 	Ana Trujillo 	Avda. de la Constitución 2222 	México D.F. 	05021 	Mexico
3 	Antonio Moreno Taquería 	Antonio Moreno 	Mataderos 2312 	México D.F. 	05023 	Mexico

And a selection from the "Suppliers" table:

SupplierID 	SupplierName 	ContactName 	Address 	City 	PostalCode 	Country
1 	Exotic Liquid 	Charlotte Cooper 	49 Gilbert St. 	London 	EC1 4SD 	UK
2 	New Orleans Cajun Delights 	Shelley Burke 	P.O. Box 78934 	New Orleans 	70117 	USA
3 	Grandma Kelly's Homestead 	Regina Murphy 	707 Oxford Rd. 	Ann Arbor 	48104 	USA


SQL UNION Example:


SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;


SQL UNION ALL: 

SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;


SQL UNION With WHERE:

SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;


SQL UNION ALL With WHERE: 

SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION ALL
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;


Another UNION Example:

SELECT 'Customer' AS Type, ContactName, City, Country
FROM Customers
UNION
SELECT 'Supplier', ContactName, City, Country
FROM Suppliers;



SQL GROUP BY Statement:

GROUP BY Syntax
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s); 


CustomerID 	CustomerName 	ContactName 	Address 	City 	PostalCode 	Country
1	Alfreds Futterkiste 	Maria Anders 	Obere Str. 57 	Berlin 	12209 	Germany
2 	Ana Trujillo Emparedados y helados 	Ana Trujillo 	Avda. de la Constitución 2222 	México D.F. 	05021 	Mexico
3 	Antonio Moreno Taquería 	Antonio Moreno 	Mataderos 2312 	México D.F. 	05023 	Mexico
4	Around the Horn 	Thomas Hardy 	120 Hanover Sq. 	London 	WA1 1DP 	UK
5 	Berglunds snabbköp 	Christina Berglund 	Berguvsvägen 8 	Luleå 	S-958 22 	Sweden


SQL GROUP BY: 

SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;


SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;


OrderID 	CustomerID 	EmployeeID 	OrderDate 	ShipperID
10248 	90 	5 	1996-07-04 	3
10249 	81 	6 	1996-07-05 	1
10250 	34 	4 	1996-07-08 	2


And a selection from the "Shippers" table:

ShipperID 	ShipperName
1 	Speedy Express
2 	United Package
3 	Federal Shipping


GROUP BY With JOIN:


SELECT Shippers.ShipperName, COUNT(Orders.OrderID) AS NumberOfOrders FROM Orders
LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID
GROUP BY ShipperName;


SQL HAVING Clause: 

HAVING Syntax
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s); 

CustomerID 	CustomerName 	ContactName 	Address 	City 	PostalCode 	Country
1	Alfreds Futterkiste 	Maria Anders 	Obere Str. 57 	Berlin 	12209 	Germany
2 	Ana Trujillo Emparedados y helados 	Ana Trujillo 	Avda. de la Constitución 2222 	México D.F. 	05021 	Mexico
3 	Antonio Moreno Taquería 	Antonio Moreno 	Mataderos 2312 	México D.F. 	05023 	Mexico
4	Around the Horn 	Thomas Hardy 	120 Hanover Sq. 	London 	WA1 1DP 	UK
5 	Berglunds snabbköp 	Christina Berglund 	Berguvsvägen 8 	Luleå 	S-958 22 	Sweden


SQL HAVING Examples

SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;

SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;

OrderID 	CustomerID 	EmployeeID 	OrderDate 	ShipperID
10248 	90 	5 	1996-07-04 	3
10249 	81 	6 	1996-07-05 	1
10250 	34 	4 	1996-07-08 	2


EmployeeID 	LastName 	FirstName 	BirthDate 	Photo 	Notes
1 	Davolio 	Nancy 	1968-12-08 	EmpID1.pic 	Education includes a BA....
2 	Fuller 	Andrew 	1952-02-19 	EmpID2.pic 	Andrew received his BTS....
3 	Leverling 	Janet 	1963-08-30 	EmpID3.pic 	Janet has a BS degree....



More HAVING Examples:


Example:

SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM (Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID)
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 10;


Example:

SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
WHERE LastName = 'Davolio' OR LastName = 'Fuller'
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 25;



SQL EXISTS Operator: 


EXISTS Syntax
SELECT column_name(s)
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition); 

ProductID 	ProductName 	SupplierID 	CategoryID 	Unit 	Price
1 	Chais 	1 	1 	10 boxes x 20 bags 	18
2 	Chang 	1 	1 	24 - 12 oz bottles 	19
3 	Aniseed Syrup 	1 	2 	12 - 550 ml bottles 	10
4 	Chef Anton's Cajun Seasoning 	2 	2 	48 - 6 oz jars 	22
5 	Chef Anton's Gumbo Mix 	2 	2 	36 boxes 	21.35



And a selection from the "Suppliers" table:

SupplierID 	SupplierName 	ContactName 	Address 	City 	PostalCode 	Country
1 	Exotic Liquid 	Charlotte Cooper 	49 Gilbert St. 	London 	EC1 4SD 	UK
2 	New Orleans Cajun Delights 	Shelley Burke 	P.O. Box 78934 	New Orleans 	70117 	USA
3 	Grandma Kelly's Homestead 	Regina Murphy 	707 Oxford Rd. 	Ann Arbor 	48104 	USA
4 	Tokyo Traders 	Yoshi Nagase 	9-8 Sekimai Musashino-shi 	Tokyo 	100 	Japan



Example:

	SELECT SupplierName
	FROM Suppliers
	WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20); 

Example:

	SELECT SupplierName
	FROM Suppliers
	WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price = 22); 



SQL ANY and ALL Operators:

ANY Syntax:

SELECT column_name(s)
FROM table_name
WHERE column_name operator ANY
  (SELECT column_name
  FROM table_name
  WHERE condition); 
  
  
ALL Syntax With SELECT:

SELECT ALL column_name(s)
FROM table_name
WHERE condition;

ALL Syntax With WHERE or HAVING:

SELECT column_name(s)
FROM table_name
WHERE column_name operator ALL
  (SELECT column_name
  FROM table_name
  WHERE condition);   
  

ProductID 	ProductName 	SupplierID 	CategoryID 	Unit 	Price
1 	Chais 	1 	1 	10 boxes x 20 bags 	18
2 	Chang 	1 	1 	24 - 12 oz bottles 	19
3 	Aniseed Syrup 	1 	2 	12 - 550 ml bottles 	10
4 	Chef Anton's Cajun Seasoning 	2 	2 	48 - 6 oz jars 	22
5 	Chef Anton's Gumbo Mix 	2 	2 	36 boxes 	21.35
6 	Grandma's Boysenberry Spread 	3 	2 	12 - 8 oz jars 	25
7 	Uncle Bob's Organic Dried Pears 	3 	7 	12 - 1 lb pkgs. 	30
8 	Northwoods Cranberry Sauce 	3 	2 	12 - 12 oz jars 	40
9 	Mishi Kobe Niku 	4 	6 	18 - 500 g pkgs. 	97


And a selection from the "OrderDetails" table:
OrderDetailID 	OrderID 	ProductID 	Quantity
1 	10248 	11 	12
2 	10248 	42 	10
3 	10248 	72 	5
4 	10249 	14 	9
5 	10249 	51 	40
6 	10250 	41 	10
7 	10250 	51 	35
8 	10250 	65 	15
9 	10251 	22 	6
10 	10251 	57 	15


SQL ANY Examples: 


Example
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity = 10); 
  
  
  
  Example
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity > 99); 
  
 Example
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity > 1000);  
  
 
 SQL ALL Examples:

The following SQL statement lists ALL the product names:
Example
SELECT ALL ProductName
FROM Products
WHERE TRUE; 
  

Example:

SELECT ProductName
FROM Products
WHERE ProductID = ALL
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity = 10); 



SQL SELECT INTO Statement: 

SELECT INTO Syntax:

Copy all columns into a new table:

SELECT *
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;

Copy only some columns into a new table:

SELECT column1, column2, column3, ...
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition; 


SQL SELECT INTO Examples

The following SQL statement creates a backup copy of Customers:

	SELECT * INTO CustomersBackup2017
	FROM Customers;

The following SQL statement uses the IN clause to copy the table into a new table in another database:

	SELECT * INTO CustomersBackup2017 IN 'Backup.mdb'
	FROM Customers;

The following SQL statement copies only a few columns into a new table:

	SELECT CustomerName, ContactName INTO CustomersBackup2017
	FROM Customers;

The following SQL statement copies only the German customers into a new table:

	SELECT * INTO CustomersGermany
	FROM Customers
	WHERE Country = 'Germany';

The following SQL statement copies data from more than one table into a new table:

	SELECT Customers.CustomerName, Orders.OrderID
	INTO CustomersOrderBackup2017
	FROM Customers
	LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;

	SELECT * INTO newtable
	FROM oldtable
	WHERE 1 = 0;




SQL INSERT INTO SELECT Statement: 

INSERT INTO SELECT Syntax

Copy all columns from one table to another table:
INSERT INTO table2
SELECT * FROM table1
WHERE condition;

Copy only some columns from one table into another table:
INSERT INTO table2 (column1, column2, column3, ...)
SELECT column1, column2, column3, ...
FROM table1
WHERE condition;


Demo Database

In this tutorial we will use the well-known Northwind sample database.

Below is a selection from the "Customers" table:
CustomerID 	CustomerName 	ContactName 	Address 	City 	PostalCode 	Country
1	Alfreds Futterkiste 	Maria Anders 	Obere Str. 57 	Berlin 	12209 	Germany
2 	Ana Trujillo Emparedados y helados 	Ana Trujillo 	Avda. de la Constitución 2222 	México D.F. 	05021 	Mexico
3 	Antonio Moreno Taquería 	Antonio Moreno 	Mataderos 2312 	México D.F. 	05023 	Mexico

And a selection from the "Suppliers" table:
SupplierID 	SupplierName 	ContactName 	Address 	City 	Postal Code 	Country
1 	Exotic Liquid 	Charlotte Cooper 	49 Gilbert St. 	Londona 	EC1 4SD 	UK
2 	New Orleans Cajun Delights 	Shelley Burke 	P.O. Box 78934 	New Orleans 	70117 	USA
3 	Grandma Kelly's Homestead 	Regina Murphy 	707 Oxford Rd. 	Ann Arbor 	48104 	USA


SQL INSERT INTO SELECT Examples

The following SQL statement copies "Suppliers" into "Customers" (the columns that are not filled with data, will contain NULL):
Example
INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country FROM Suppliers;

The following SQL statement copies "Suppliers" into "Customers" (fill all columns):
Example
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
SELECT SupplierName, ContactName, Address, City, PostalCode, Country FROM Suppliers;

The following SQL statement copies only the German suppliers into "Customers":
Example
INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country FROM Suppliers
WHERE Country='Germany';


SQL CASE Expression: 

CASE Syntax
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END; 



Demo Database

Below is a selection from the "OrderDetails" table in the Northwind sample database:
OrderDetailID 	OrderID 	ProductID 	Quantity
1 	10248 	11 	12
2 	10248 	42 	10
3 	10248 	72 	5
4 	10249 	14 	9
5 	10249 	51 	40


SQL CASE Examples

The following SQL goes through conditions and returns a value when the first condition is met:
Example
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails; 


Example:

	SELECT CustomerName, City, Country
	FROM Customers
	ORDER BY
	(CASE
	    WHEN City IS NULL THEN Country
	    ELSE City
	END); 


SQL IFNULL(), ISNULL(), COALESCE(), and NVL() Functions: 

P_Id 	ProductName 	UnitPrice 	UnitsInStock 	UnitsOnOrder
1 	Jarlsberg 	10.45 	16 	15
2 	Mascarpone 	32.56 	23 	 
3 	Gorgonzola 	15.67 	9 	20

Look at the following SELECT statement:
SELECT ProductName, UnitPrice * (UnitsInStock + UnitsOnOrder)
FROM Products;

Solutions

MySQL

The MySQL IFNULL() function lets you return an alternative value if an expression is NULL:
SELECT ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder, 0))
FROM Products;

or we can use the COALESCE() function, like this:
SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products; 

SQL Server

The SQL Server ISNULL() function lets you return an alternative value when an expression is NULL:
SELECT ProductName, UnitPrice * (UnitsInStock + ISNULL(UnitsOnOrder, 0))
FROM Products;

or we can use the COALESCE() function, like this:
SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products;

MS Access

The MS Access IsNull() function returns TRUE (-1) if the expression is a null value, otherwise FALSE (0):
SELECT ProductName, UnitPrice * (UnitsInStock + IIF(IsNull(UnitsOnOrder), 0, UnitsOnOrder))
FROM Products;

Oracle

The Oracle NVL() function achieves the same result:
SELECT ProductName, UnitPrice * (UnitsInStock + NVL(UnitsOnOrder, 0))
FROM Products;

or we can use the COALESCE() function, like this:
SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products; 



SQL Stored Procedures for SQL Server: 




What is a Stored Procedure?

A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again.


Stored Procedure Syntax
CREATE PROCEDURE procedure_name
AS
sql_statement
GO; 


Execute a Stored Procedure
EXEC procedure_name; 


Demo Database

Below is a selection from the "Customers" table in the Northwind sample database:
CustomerID 	CustomerName 	ContactName 	Address 	City 	PostalCode 	Country
1

	Alfreds Futterkiste 	Maria Anders 	Obere Str. 57 	Berlin 	12209 	Germany
2 	Ana Trujillo Emparedados y helados 	Ana Trujillo 	Avda. de la Constitución 2222 	México D.F. 	05021 	Mexico
3 	Antonio Moreno Taquería 	Antonio Moreno 	Mataderos 2312 	México D.F. 	05023 	Mexico
4

	Around the Horn 	Thomas Hardy 	120 Hanover Sq. 	London 	WA1 1DP 	UK
5 	Berglunds snabbköp 	Christina Berglund 	Berguvsvägen 8 	Luleå 	S-958 22 	Sweden


Stored Procedure Example

The following SQL statement creates a stored procedure named "SelectAllCustomers" that selects all records from the "Customers" table:
Example
CREATE PROCEDURE SelectAllCustomers
AS
SELECT * FROM Customers
GO;

Execute the stored procedure above as follows:
Example
EXEC SelectAllCustomers;

Stored Procedure With One Parameter

The following SQL statement creates a stored procedure that selects Customers from a particular City from the "Customers" table:
Example
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
AS
SELECT * FROM Customers WHERE City = @City
GO;

Execute the stored procedure above as follows:
Example
EXEC SelectAllCustomers @City = 'London';
Stored Procedure With Multiple Parameters

Setting up multiple parameters is very easy. Just list each parameter and the data type separated by a comma as shown below.

The following SQL statement creates a stored procedure that selects Customers from a particular City with a particular PostalCode from the "Customers" table:
Example
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30), @PostalCode nvarchar(10)
AS
SELECT * FROM Customers WHERE City = @City AND PostalCode = @PostalCode
GO;

Execute the stored procedure above as follows:

Example:

	EXEC SelectAllCustomers @City = 'London', @PostalCode = 'WA1 1DP';



SQL Comments:

Example
--Select all:
SELECT * FROM Customers;


Example
SELECT * FROM Customers -- WHERE City='Berlin'; 

--SELECT * FROM Customers;
SELECT * FROM Products;


Example
/*Select all the columns
of all the records
in the Customers table:*/
SELECT * FROM Customers;

Example
/*SELECT * FROM Customers;
SELECT * FROM Products;
SELECT * FROM Orders;
SELECT * FROM Categories;*/
SELECT * FROM Suppliers;

Example
SELECT CustomerName, /*City,*/ Country FROM Customers;

Example
SELECT * FROM Customers WHERE (CustomerName LIKE 'L%'
OR CustomerName LIKE 'R%' /*OR CustomerName LIKE 'S%'
OR CustomerName LIKE 'T%'*/ OR CustomerName LIKE 'W%')
AND Country='USA'
ORDER BY CustomerName; 


































 :end: 
 
 
 
 
 
 
 [Go To Top](#top)
<a name="sql_advanced_queries"></a>
 # SQL Advanced Queries
 
 
 
 
 
 :end:
 
 
 
 
 
 
 

[Go To Top](#top)
<a name="sql_interviews_questions_14"></a>
 # Top 14 Frequently asked SQL Query Interview Questions
 
 
Question 1: SQL Query to find the second highest salary of Employee

    SELECT MAX(Salary) 
    FROM Employee 
    WHERE Salary NOT IN (select MAX(Salary) from Employee ); 


See How to find the second highest salary in SQL for more ways to solve this problem.


Question 2: SQL Query to find Max Salary from each department.

    SELECT DeptID, MAX(Salary) 
    FROM Employee 
    GROUP BY DeptID. 


Here is the query

    SELECT DeptName, MAX(Salary) 
    FROM Employee e RIGHT JOIN Department d 
    ON e.DeptId = d.DeptID 
    GROUP BY DeptName;


Question 3: Write SQL Query to display the current date?

    SELECT GetDate(); 


Question 4: Write an SQL Query to check whether the date passed to Query is the date of the given format or not?

    SELECT  ISDATE('1/08/13') AS "MM/DD/YY"; 


It will return 0 because the passed date is not in the correct format.


Question 5: Write an SQL Query to print the name of the distinct employee whose DOB is between 01/01/1960 to 31/12/1975.

    SELECT DISTINCT EmpName 
    FROM Employees 
    WHERE DOB BETWEEN ‘01/01/1960’ AND ‘31/12/1975’;



Question 6: Write an SQL Query to find the number of employees according to gender whose DOB is between 01/01/1960 to 31/12/1975.


    SELECT COUNT(*), sex 
    FROM Employees  
    WHERE DOB BETWEEN '01/01/1960' AND '31/12/1975' 
    GROUP BY sex;


Question 7: Write an SQL Query to find an employee whose salary is equal to or greater than 10000.
 

    SELECT EmpName FROM  Employees WHERE  Salary>=10000;



Question 8: Write an SQL Query to find the name of an employee whose name Start with ‘M’

    SELECT * FROM Employees WHERE EmpName like 'M%';


Question 9: find all Employee records containing the word "Joe", regardless of whether it was stored as JOE, Joe, or joe.

    SELECT * from Employees  WHERE  UPPER(EmpName) like '%JOE%';



Question 10: Write an SQL Query to find the year from date.

    SELECT YEAR(GETDATE()) as "Year";


Question 11: Write SQL Query to find duplicate rows in a database? and then write SQL query to delete them?

    SELECT * FROM emp a 
    WHERE rowid = (SELECT MAX(rowid) 
    FROM EMP b 
    WHERE a.empno=b.empno)


to Delete:

    DELETE FROM emp a 
    WHERE rowid != (SELECT MAX(rowid) FROM emp b WHERE a.empno=b.empno);


Question 12: There is a table which contains two columns Student and Marks, you need to find all the students, whose marks are greater than average marks i.e. list of above-average students.

    SELECT student, marks 
    FROM table 
    WHERE marks > SELECT AVG(marks) from table)


SQL Query Interview Questions and Answers


Question 13: How do you find all employees who are also managers?
You have given a standard employee table with an additional column mgr_id, which contains the employee id of the manager.
Employee department SQL Query question

    SELECT e.name, m.name 
    FROM Employee e, Employee m 
    WHERE e.mgr_id = m.emp_id;


this will show employee name and manager name in two columns like

    name  manager_name
    John   David

Question 14: You have a composite index of three columns, and you only provide the value of two columns in the WHERE clause of a select query? Will Index be used for this operation? For example, if Index is on EmpId, EmpFirstName, and EmpSecondName and you write a query like

    SELECT * FROM Employee WHERE EmpId=2 and EmpFirstName='Radhe'


  
 :end:






[Go To Top](#top)
<a name="sql_interviews_questions_40"></a>
         
# Top 40 SQL Query Interview Questions and Answers for Practice


Table – EmployeeDetails:

    EmpId	 FullName	    ManagerId	  DateOfJoining	 City
    121  	 John Snow	   321	        01/31/2019	    Toronto
    321	   Walter White	986	        01/30/2020	    California
    421	   Kuldeep Rana	876	        27/11/2021	    New Delhi


Table – EmployeeSalary:

    EmpId	Project	Salary	 Variable
    121	  P1	     8000	   500
    321	  P2	     10000	  1000
    421	  P1	     12000	  0

SQL Query Interview Questions for Freshers: 


### Ques.1. Write an SQL query to fetch the EmpId and FullName of all the employees working under the Manager with id – ‘986’.

    SELECT  EmpId, FullName
    FROM EmployeeDetails
    WHERE ManagerId = 986;



###  Ques.2. Write an SQL query to fetch the different projects available from the EmployeeSalary table.

    SELECT DISTINCT(Project)
    FROM EmployeeSalary;


### Ques.3. Write an SQL query to fetch the count of employees working in project ‘P1’.

    SELECT COUNT(*) 
    FROM EmployeeSalary 
    WHERE Project = 'P1';



### Ques.4. Write an SQL query to find the maximum, minimum, and average salary of the employees.

    SELECT Max(Salary), 
    Min(Salary), 
    AVG(Salary) 
    FROM EmployeeSalary;


### Ques.5. Write an SQL query to find the employee id whose salary lies in the range of 9000 and 15000.

    SELECT EmpId, Salary
    FROM EmployeeSalary
    WHERE Salary BETWEEN 9000 AND 15000;



### Ques.6. Write an SQL query to fetch those employees who live in Toronto and work under the manager with ManagerId – 321.

    SELECT EmpId, City, ManagerId
    FROM EmployeeDetails
    WHERE City='Toronto' AND ManagerId='321';

### Ques.7. Write an SQL query to fetch all the employees who either live in California or work under a manager with ManagerId – 321.

    SELECT EmpId, City, ManagerId
    FROM EmployeeDetails
    WHERE City='California' OR ManagerId='321';
    

### Ques.8. Write an SQL query to fetch all those employees who work on Projects other than P1.

    SELECT EmpId
    FROM EmployeeSalary
    WHERE NOT Project='P1';


Or using the ‘not equal to’ operator-

    SELECT EmpId
    FROM EmployeeSalary
    WHERE Project <> 'P1';

For the difference between NOT and <> SQL operators, check this link – Difference between the NOT and != operators.



### Ques.9. Write an SQL query to display the total salary of each employee adding the Salary with Variable value.

    SELECT EmpId,
    Salary+Variable as TotalSalary 
    FROM EmployeeSalary;



### Ques.10. Write an SQL query to fetch the employees whose name begins with any two characters, followed by a text “hn” and ends with any sequence of characters.

    SELECT FullName
    FROM EmployeeDetails
    WHERE FullName LIKE ‘__hn%’;


### Ques.11. Write an SQL query to fetch all the EmpIds which are present in either of the tables – ‘EmployeeDetails’ and ‘EmployeeSalary’.


    SELECT EmpId FROM EmployeeDetails
    UNION 
    SELECT EmpId FROM EmployeeSalary;



### Ques.12. Write an SQL query to fetch common records between two tables.

    SELECT * FROM EmployeeSalary
    INTERSECT
    SELECT * FROM ManagerSalary;


MySQL – Since MySQL doesn’t have INTERSECT operator so we can use the subquery-

    SELECT *
    FROM EmployeeSalary
    WHERE EmpId IN 
    (SELECT EmpId from ManagerSalary);


### Ques.13. Write an SQL query to fetch records that are present in one table but not in another table.

    SELECT * FROM EmployeeSalary
    MINUS
    SELECT * FROM ManagerSalary;


MySQL – Since MySQL doesn’t have a MINUS operator so we can use LEFT join-

    SELECT EmployeeSalary.*
    FROM EmployeeSalary
    LEFT JOIN
    ManagerSalary USING (EmpId)
    WHERE ManagerSalary.EmpId IS NULL;



### Ques.14. Write an SQL query to fetch the EmpIds that are present in both the tables –   ‘EmployeeDetails’ and ‘EmployeeSalary.

    SELECT EmpId FROM 
    EmployeeDetails 
    where EmpId IN 
    (SELECT EmpId FROM EmployeeSalary);



### Ques.15. Write an SQL query to fetch the EmpIds that are present in EmployeeDetails but not in EmployeeSalary.


    SELECT EmpId FROM 
    EmployeeDetails 
    where EmpId Not IN 
    (SELECT EmpId FROM EmployeeSalary);



### Ques.16. Write an SQL query to fetch the employee’s full names and replace the space with ‘-’.

    SELECT REPLACE(FullName, ' ', '-') 
    FROM EmployeeDetails;



### Ques.17. Write an SQL query to fetch the position of a given character(s) in a field.

    SELECT INSTR(FullName, 'Snow')
    FROM EmployeeDetails;



### Ques.18. Write an SQL query to display both the EmpId and ManagerId together.

    SELECT CONCAT(EmpId, ManagerId) as NewId
    FROM EmployeeDetails;


### Ques.19. Write a query to fetch only the first name(string before space) from the FullName column of the EmployeeDetails table.

MySQL – using MID

   SELECT MID(FullName, 1, LOCATE(' ',FullName)) 
   FROM EmployeeDetails;


SQL Server – using SUBSTRING

    SELECT SUBSTRING(FullName, 1, CHARINDEX(' ',FullName)) 
    FROM EmployeeDetails;



### Ques.20. Write an SQL query to uppercase the name of the employee and lowercase the city values.

    SELECT UPPER(FullName), LOWER(City) 
    FROM EmployeeDetails;


### Ques.21. Write an SQL query to find the count of the total occurrences of a particular character – ‘n’ in the FullName field.

    SELECT FullName, 
    LENGTH(FullName) - LENGTH(REPLACE(FullName, 'n', ''))
    FROM EmployeeDetails;



### Ques.22. Write an SQL query to update the employee names by removing leading and trailing spaces.

    UPDATE EmployeeDetails 
    SET FullName = LTRIM(RTRIM(FullName));


### Ques.23. Fetch all the employees who are not working on any project.

    SELECT EmpId 
    FROM EmployeeSalary 
    WHERE Project IS NULL;


### Ques.24. Write an SQL query to fetch employee names having a salary greater than or equal to 5000 and less than or equal to 10000.

    SELECT FullName 
    FROM EmployeeDetails 
    WHERE EmpId IN 
    (SELECT EmpId FROM EmployeeSalary 
    WHERE Salary BETWEEN 5000 AND 10000);



### Ques.25. Write an SQL query to find the current date-time.

MySQL-

    SELECT NOW();


SQL Server-

    SELECT getdate();


Oracle-

    SELECT SYSDATE FROM DUAL;


### Ques.26. Write an SQL query to fetch all the Employee details from the EmployeeDetails table who joined in the Year 2020.

    SELECT * FROM EmployeeDetails
    WHERE DateOfJoining BETWEEN '2020/01/01'
    AND '2020/12/31';


Also, we can extract the year part from the joining date (using YEAR in MySQL)-

    SELECT * FROM EmployeeDetails 
    WHERE YEAR(DateOfJoining) = '2020';


### Ques.27. Write an SQL query to fetch all employee records from the EmployeeDetails table who have a salary record in the EmployeeSalary table.

    SELECT * FROM EmployeeDetails E
    WHERE EXISTS
    (SELECT * FROM EmployeeSalary S 
    WHERE  E.EmpId = S.EmpId);


### Ques.28. Write an SQL query to fetch the project-wise count of employees sorted by project’s count in descending order.

    SELECT Project, count(EmpId) EmpProjectCount
    FROM EmployeeSalary
    GROUP BY Project
    ORDER BY EmpProjectCount DESC;


### Ques.29. Write a query to fetch employee names and salary records. Display the employee details even if the salary record is not present for the employee.

    SELECT E.FullName, S.Salary 
    FROM EmployeeDetails E 
    LEFT JOIN 
    EmployeeSalary S
    ON E.EmpId = S.EmpId;



### Ques.30. Write an SQL query to join 3 tables.

    SELECT column1, column2
    FROM TableA
    JOIN TableB ON TableA.Column3 = TableB.Column3
    JOIN TableC ON TableA.Column4 = TableC.Column4;


SQL Query Interview Questions for Experienced: 


### Ques. 31. Write an SQL query to fetch all the Employees who are also managers from the EmployeeDetails table.

    SELECT DISTINCT E.FullName
    FROM EmployeeDetails E
    INNER JOIN EmployeeDetails M
    ON E.EmpID = M.ManagerID;


### Ques.32. Write an SQL query to fetch duplicate records from EmployeeDetails (without considering the primary key – EmpId).

    SELECT FullName, ManagerId, DateOfJoining, City, COUNT(*)
    FROM EmployeeDetails
    GROUP BY FullName, ManagerId, DateOfJoining, City
    HAVING COUNT(*) > 1;



### Ques.33. Write an SQL query to remove duplicates from a table without using a temporary table.


    DELETE E1 FROM EmployeeDetails E1
    INNER JOIN EmployeeDetails E2 
    WHERE E1.EmpId > E2.EmpId 
    AND E1.FullName = E2.FullName 
    AND E1.ManagerId = E2.ManagerId
    AND E1.DateOfJoining = E2.DateOfJoining
    AND E1.City = E2.City;


### Ques.34. Write an SQL query to fetch only odd rows from the table.

    SELECT * FROM EmployeeDetails 
    WHERE MOD (EmpId, 2) <> 0;


In case we don’t have such a field then we can use the below queries.

Using Row_number in SQL server and checking that the remainder when divided by 2 is 1-

    SELECT E.EmpId, E.Project, E.Salary
    FROM (
        SELECT *, Row_Number() OVER(ORDER BY EmpId) AS RowNumber
        FROM EmployeeSalary
    ) E
    WHERE E.RowNumber % 2 = 1;


Using a user-defined variable in MySQL-

    SELECT *
    FROM (
          SELECT *, @rowNumber := @rowNumber+ 1 rn
          FROM EmployeeSalary
          JOIN (SELECT @rowNumber:= 0) r
         ) t 
    WHERE rn % 2 = 1;



### Ques.35. Write an SQL query to fetch only even rows from the table.

    SELECT * FROM EmployeeDetails 
    WHERE MOD (EmpId, 2) = 0;


In case we don’t have such a field then we can use the below queries.

Using Row_number in SQL server and checking that the remainder, when divided by 2, is 1-

    SELECT E.EmpId, E.Project, E.Salary
    FROM (
        SELECT *, Row_Number() OVER(ORDER BY EmpId) AS RowNumber
        FROM EmployeeSalary
    ) E
    WHERE E.RowNumber % 2 = 0;


Using a user-defined variable in MySQL-

    SELECT *
    FROM (
          SELECT *, @rowNumber := @rowNumber+ 1 rn
          FROM EmployeeSalary
          JOIN (SELECT @rowNumber:= 0) r
         ) t 
    WHERE rn % 2 = 0;



### Ques.36. Write an SQL query to create a new table with data and structure copied from another table.
Ans.

    CREATE TABLE NewTable 
    SELECT * FROM EmployeeSalary;



### Ques.37. Write an SQL query to create an empty table with the same structure as some other table.

    CREATE TABLE NewTable 
    SELECT * FROM EmployeeSalary where 1=0;



### Ques.38. Write an SQL query to fetch top n records.

    SELECT *
    FROM EmployeeSalary
    ORDER BY Salary DESC LIMIT N;


In SQL server using TOP command-

    SELECT TOP N *
    FROM EmployeeSalary
    ORDER BY Salary DESC;



### Ques.39. Write an SQL query to find the nth highest salary from a table.
Ans. Using Top keyword (SQL Server)-

    SELECT TOP 1 Salary
    FROM (
          SELECT DISTINCT TOP N Salary
          FROM Employee
          ORDER BY Salary DESC
          )
    ORDER BY Salary ASC;


Using limit clause(MySQL)-

    SELECT Salary
    FROM Employee
    ORDER BY Salary DESC LIMIT N-1,1;


### Ques.40. Write SQL query to find the 3rd highest salary from a table without using the TOP/limit keyword.

    SELECT Salary
    FROM EmployeeSalary Emp1
    WHERE 2 = (
                    SELECT COUNT( DISTINCT ( Emp2.Salary ) )
                    FROM EmployeeSalary Emp2
                    WHERE Emp2.Salary > Emp1.Salary
                )


For nth highest salary-

    SELECT Salary
    FROM EmployeeSalary Emp1
    WHERE N-1 = (
                    SELECT COUNT( DISTINCT ( Emp2.Salary ) )
                    FROM EmployeeSalary Emp2
                    WHERE Emp2.Salary > Emp1.Salary
                )




:end: 








[Go To Top](#top)
<a name="sql_interviews_questions_30"></a>
         
# SQL Interviews Questions
         
         
Patients Table:

Patient ID	Patient Name	Sex	Age	Address	                                 Postal Code	  State	      Country	RegDate	   DoctorID<br>
01	        Sheela	      F	  23	 Flat no 201, Vasavi Heights, Yakutapura 	500023	       Telangana	  India	  03/03/2020	142<br>
02	        Rehan	       M	  21	 Building no 2, Yelahanka	                560063	       Karnataka	  India	  13/11/2020	211<br>
03	        Anay        	M	  56	 H No 1, Panipat	                         132140	       Haryana	    India	  12/12/2021	142<br>
04	        Mahira	      F	  42	 House no 12, Gandhinagar	                382421	       Gujarat	    India	  28/01/2022	345<br>
05	        Nishant     	M	  12	 Sunflower Heights, Thane	                400080	       Maharashtra	India	  05/01/2022	131<br>


PatientsCheckup Table: 

Patient ID	 BP	      Weight	 Consultation Fees<br>

01	         121/80	  67	     300 <br>
02	         142/76	  78	     400 <br>
03	         151/75	  55	     300 <br>
04	         160/81	  61	     550 <br>
05	         143/67	  78	     700<br>


### Q1.  Write an SQL query to fetch the current date-time from the system.

 TO fetch the CURRENT DATE IN SQL Server
 
     SELECT GETDATE();
   
 TO fetch the CURRENT DATE IN MYSQL
 
     SELECT NOW();
   
 TO fetch the CURRENT DATE IN Oracle
 
     SELECT SYSDATE FROM DUAL();

### Q2. Write a SQL query to fetch the PatientName in uppercase and state as lowercase. Also use the ALIAS name for the result-set as PatName and NewState.

   TO fetch the CURRENT DATE IN SQL Server
   
     SELECT GETDATE();
     
   TO fetch the CURRENT DATE IN MYSQL
   
     SELECT NOW();
     
   TO fetch the CURRENT DATE IN Oracle
   
     SELECT SYSDATE FROM DUAL();

### Q3. Find the Nth highest consultation fees from the PatientsCheckup table with and without using the TOP/LIMIT keywords.

Nth highest consultation fees from the PatientsCheckup table with using the TOP keywords

    SELECT TOP 1 ConsultationFees
    FROM(
    SELECT TOP N ConsultationFees
    FROM PatientsCheckup
    ORDER BY ConsultationFees DESC) AS FEES
    ORDER BY ConsultationFees ASC;

The Nth highest consultation fees from the PatientsCheckup table using the LIMIT keywords.

    <code>
    SELECT ConsultationFees
    FROM PatientsCheckup
    ORDER BY ConsultationFees DESC LIMIT N-1,1;
    </code>

Nth highest consultation fees from the PatientsCheckup table without using the TOP/LIMIT keywords.

    <code>
    SELECT ConsultationFees
    FROM PatientsCheckup F1
    WHERE N-1 = (
          SELECT COUNT( DISTINCT ( F2.ConsultationFees ) )
          FROM PatientsCheckup F2
          WHERE F2.ConsultationFees >  F1.ConsultationFees );
    </code>

### Q4. Write a query to fetch top N records using the TOP/LIMIT, ordered by ConsultationFees.

TOP Command – SQL Server

    SELECT TOP N * FROM PatientsCheckup ORDER BY ConsultationFees DESC;
 
LIMIT Command - MySQL

    SELECT * FROM PatientsCheckup ORDER BY ConsultationFees DESC LIMIT N;

### Q5. Write a SQL query to create a table where the structure is copied from other table.

      Create an Empty Table
      Create a table consisting data

To create an Empty table

    CREATE TABLE NewPatientsTable 
    SELECT * FROM Patients WHERE 1=0;



Create a table consisting of data

-USING SELECT command

    SELECT * INTO NewPatientsTable FROM Patients WHERE 1 = 0;

 – USING CREATE command IN MySQL 
 
    CREATE TABLE NewPatientsTable AS SELECT * FROM Patients;


### Q6. Write a query to fetch even and odd rows from a table.

If you have an auto-increment field like PatientID then you can use the MOD() function:

  Fetch even rows using MOD() function:

    SELECT * FROM Patients WHERE MOD(PatientID,2)=0;

  Fetch odd rows using MOD() function:

    SELECT * FROM Patients WHERE MOD(PatientID,2)=1;

In case there are no auto-increment fields then you can use the Row_number in SQL Server or a user-defined variable in MySQL. Then, check the remainder when divided by 2.

Fetch even rows in SQL Server

    SELECT * FROM (
        SELECT *, ROW_NUMBER() OVER(ORDER BY PatientId) AS RowNumber
        FROM Patients
    ) P
    WHERE P.RowNumber % 2 = 0;

    Fetch even rows in MySQL

    SELECT * FROM (
          SELECT *, @rowNumber := @rowNumber+ 1 rn
          FROM Patients
          JOIN (SELECT @rowNumber:= 0) r
         ) p 
    WHERE rn % 2 = 0;

In case you wish to find the odd rows, then the remainder when divided by 2 should be 1.

### Q7. Write an SQL query to fetch duplicate records from Patients, without considering the primary key.

    SELECT PatientName, DoctorID, RegDate, State, COUNT(*)
    FROM Patients
    GROUP BY PatientName, DoctorID, RegDate, State
    HAVING COUNT(*) > 1;

### Q8. Write a query to fetch the number of patients whose weight is greater than 68.

    SELECT COUNT(*) FROM PatientsCheckup WHERE Weight > '68';

### Q9. Write a query to retrieve the list of patients from the same state.

    SELECT DISTINCT P.PatientID, P.PatientName, P.State
    FROM Patients P, Patient P1
    WHERE P.State = P1.State AND P.PatientID != P1.PatientID;

### Q10. Write a query to retrieve two minimum and maximum consultation fees from the PatientsCheckup Table.

  
  – TWO MINIMUM CONSULTATION FEES
  
      SELECT DISTINCT ConsultationFees FROM PatientsCheckup P1
       WHERE 2 >= (SELECT COUNT(DISTINCT ConsultationFees)FROM PatientsCheckup P2
        WHERE P1.ConsultationFees >= P2.ConsultationFees) ORDER BY P1.SConsultationFees DESC;

  – TWO MAXIMUM CONSULTATION FEES

      SELECT DISTINCT ConsultationFees FROM PatientsCheckup P1
       WHERE 2 >= (SELECT COUNT(DISTINCT ConsultationFees)FROM PatientsCheckup P2
        WHERE P1.ConsultationFees <= P2.ConsultationFees) ORDER BY P1.ConsultationFees DESC;



### Q11. Write a query to fetch patient details along with the weight fees, even if the details are missing.

    SELECT P.PatientName, C.ConsultationFees
    FROM Patients P 
    LEFT JOIN 
    PatientsCheckup C
    ON P.PatientId = C.PatientId;

### Q12. Write a SQL query to fetch doctor wise count of patients sorted by the doctors.

    SELECT DoctorID, COUNT(PatientID) AS DocPat
    FROM Patients GROUP BY DoctorID
    ORDER BY DocPat;

### Q13. Write a SQL query to fetch the first and last record of the Patients table.

  –FETCH FIRST RECORD
  
      SELECT * FROM Patients WHERE PatientID = (SELECT MIN(PatientID) FROM Patients);

  –FETCH LAST RECORD
  
      SELECT * FROM Patients WHERE PatientID = (SELECT MAX(PatientID) FROM Patients);

### Q14. Write a SQL query to fetch consultation fees – wise count and sort them in descending order.

    SELECT ConsultationFees, COUNT(PatientId) CFCount
    FROM PatientsCheckup 
    GROUP BY ConsultationFees
    ORDER BY CFCount DESC;

### Q15. Write a SQL query to retrieve patient details from the Patients table who have a weight in the PatientsCheckup table.

    SELECT * FROM Patients P
    WHERE EXISTS
    (SELECT * FROM PatientsCheckup C WHERE P.PatientID = C.PatientID);

### Q16. Write a SQL query to retrieve the last 2 records from the Patients table.

    SELECT * FROM Patients WHERE
    PatientID <=2 UNION SELECT * FROM
    (SELECT * FROM Patients P ORDER BY P.PatientID DESC)
    AS P1 WHERE P1.PatientID <=2;

### Q17. Write a SQL query  to find all the patients who joined in the year 2022.

–USING BETWEEN

      SELECT * FROM Patients  
      WHERE RegDate BETWEEN '2021/01/01' AND '2021/12/31';

  – USING YEAR

      SELECT * FROM Patients WHERE YEAR(RegDate ) = '2021'; 

### Q18. Write a SQL query to fetch 50% records from the PatientsCheckup table.

    SELECT *
    FROM PatientsCheckup WHERE
    PatientID <= (SELECT COUNT(PatientD)/2 FROM PatientsCheckup);

### Q19. Write a query to find those patients who have paid consultation fees between 400 to 700.

    SELECT * FROM Patients WHERE PatientID IN   
    (SELECT PatientID FROM PatientsCheckup WHERE ConsultationFees BETWEEN '400' AND '700');


### Q20. Write a query to update the patient names by removing the leading and trailing spaces.

    UPDATE Patients 
    SET PatientName = LTRIM(RTRIM(PatientName));

### Q21. Write a query to add email validation to your database.

    SELECT email FROM Patients WHERE NOT REGEXP_LIKE(email, ‘[A-Z0-9._%+-]+@[A-Z0-9.-]+.[A-Z]{2,4}’, ‘i’);

### Q22. Write a query to find all patient names whose name:

    Begin with A
    Ends with S and contains 3 alphabets
    Staying in the state Telangana

      SELECT * FROM Patients WHERE PatientName LIKE 'A%';
      SELECT * FROM Patients WHERE PatientName LIKE '___S';
      SELECT * FROM Patients WHERE State LIKE 'Telangana%’;

### Q23. Write a SQL query to fetch details of all patients excluding patients with name  “Sheela” and “Anay”.

    SELECT * FROM Patients WHERE PatientName NOT IN ('Sheela','Anay'); 

### Q24. Write a query to fetch the total count of occurrences of a particular character – ‘x’ in the PatientName.

    SELECT PatientName, PatientID 
    LENGTH(PatientName) - LENGTH(REPLACE(PatientName, 'x', ''))
    FROM Patients;

### Q25. Write a query to retrieve the first three characters of  PatientName from the Patients table.

    SELECT SUBSTRING(PatientName, 1, 3) FROM Patients; 

### Q26. Write a query to fetch only the Address (string before space).

USING the MID FUNCTION IN MySQL

    SELECT MID(Address, 0, LOCATE(' ',Address)) FROM Patients;
 
USING SUBSTRING

    SELECT SUBSTRING(Address, 1, CHARINDEX(' ',Address)) FROM Patients;

### Q27. Write a query to combine Address and state into a new column – NewAddress.

    SELECT CONCAT(Address, ' ', State) AS 'NewAddress' FROM Patients; 

### Q28. Write a query to fetch PatientIDs  which are present in: 

    Both tables
    One of the table. Let us say, patients present in Patients and not in the PatientsCheckup table.

  –Present IN BOTH TABLES
  
      SELECT PatientId FROM Patients 
      WHERE PatientId IN 
      (SELECT PatientId FROM PatientsCheckup);

  – Present IN One OF the TABLE
  
      SELECT PatientId FROM Patients 
      WHERE PatientId NOT IN 
      (SELECT PatientId FROM PatientsCheckup);

### Q29. Write a query to find the number of patients whose RegDate is between 01/04/2021 to 31/12/2022 and are grouped according to state.

    SELECT COUNT(*), State FROM Patients WHERE RegDate BETWEEN '01/04/2021' AND '31/12/2022' GROUP BY State;

### Q30. Write a query to fetch all records from the Patients table; ordered by PatientName in ascending order, State in descending order.

    SELECT * FROM Patients ORDER BY PatientName ASC, State DESC;



:end:




<a name="top"></a>
<a name="more_examples_on_highest_salarary"></a>
# More Examples On Highest Salary
____
More examples on Highest Salary:

Below is simple query to find the employee whose salary is highest. 

    select *from employee where salary=(select Max(salary) from employee);

We can nest the above query to find the second largest salary. 

    select *from employee 
    group by salary 
    order by  salary desc limit 1,1;

There are other ways :

    SELECT name, MAX(salary) AS salary 
    FROM employee 
    WHERE salary IN
    (SELECT salary FROM employee MINUS SELECT MAX(salary) 
    FROM employee); 

 

    SELECT name, MAX(salary) AS salary 
    FROM employee 
    WHERE salary <> (SELECT MAX(salary) 
    FROM employee);
    
    IN SQL Server using Common Table Expression or CTE, we can find the second highest salary: 

    WITH T AS
    (
    SELECT *
       DENSE_RANK() OVER (ORDER BY Salary Desc) AS Rnk
    FROM Employees
    )
    SELECT Name
    FROM T
    WHERE Rnk=2;

How to find the third largest salary? 
Simple, we can do one more nesting.  

    SELECT name, MAX(salary) AS salary
      FROM employee
     WHERE salary < (SELECT MAX(salary) 
                     FROM employee
                     WHERE salary < (SELECT MAX(salary)
                     FROM employee)
                    ); 

Note that instead of nesting for second, third, etc largest salary, we can find nth salary using general query like in MySQL: 

    SELECT salary 
    FROM employee 
    ORDER BY salary desc limit n-1,1

    SELECT name, salary
    FROM employee A
    WHERE n-1 = (SELECT count(1) 
                 FROM employee B 
                 WHERE B.salary>A.salary)

If multiple employee have same salary. 
Suppose you have to find 4th highest salary 

    SELECT * FROM employee 
    WHERE salary= (SELECT DISTINCT(salary) 
    FROM employee ORDER BY salary DESC LIMIT 3,1);

Generic query will be 

    SELECT * FROM employee 
    WHERE salary= (SELECT DISTINCT(salary) 
    FROM employee ORDER BY salary DESC LIMIT n-1,1);


#EMPLOYEE WITH HIGHEST SALARY

    SELECT name, salary FROM employee ORDER BY salary DESC LIMIT 1; 

#EMPLOYEE WITH SECOND HIGHEST SALARY

    SELECT name, salary FROM employee WHERE salary < (SELECT MAX(salary) FROM employee) ORDER BY sal DESC LIMIT 1;

#EMPLOYEE WITH Nth HIGHEST SALARY

    SELECT name, salary FROM employee ORDER BY salary DESC LIMIT (N-1), 1;

:end: 
    















<a name="bottom"></a>
