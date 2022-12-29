# SQL Queries

$$\color{purple}{SQL \ Queries}$$

:link:[Home](all-file-links.md)     


<a name="top"></a>
 [Go To Bottom](#bottom)
 
 
# Topics

   [Go To Top](#top)
   
   [Top 14 Frequently asked SQL Query Interview Questions](#sql_interviews_questions_14)

   [Top 40 SQL Query Interview Questions and Answers for Practice](#sql_interviews_questions_40)

   [30 SQL Interviews Questions](#sql_interviews_questions_30)


____
Examples On Highest Salary:

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




    _____
    
    
    
    



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






<a name="bottom"></a>
