# SQL Queries

$$\color{purple}{SQL \ Queries}$$

:link:[Home](all-file-links.md)     


<a name="top"></a>
 [Go To Bottom](#bottom)
 
 
# Topics

   [Go To Top](#top)
   
   [Top 40 SQL Query Interview Questions and Answers for Practice](#sql_interviews_questions_40)

   [30 SQL Interviews Questions](#sql_interviews_questions_30)








[Go To Top](#top)
<a name="sql_interviews_questions_40"></a>
         
# Top 40 SQL Query Interview Questions and Answers for Practice
    
    https://artoftesting.com/sql-queries-for-interview



Table – EmployeeDetails:

EmpId	FullName	ManagerId	DateOfJoining	City
121	John Snow	321	01/31/2019	Toronto
321	Walter White	986	01/30/2020	California
421	Kuldeep Rana	876	27/11/2021	New Delhi


Table – EmployeeSalary:

EmpId	Project	Salary	Variable
121	P1	8000	500
321	P2	10000	1000
421	P1	12000	0


Ques.1. Write an SQL query to fetch the EmpId and FullName of all the employees working under the Manager with id – ‘986’.
Ans. We can use the EmployeeDetails table to fetch the employee details with a where clause for the manager-

SELECT  EmpId, FullName
FROM EmployeeDetails
WHERE ManagerId = 986;



Ques.2. Write an SQL query to fetch the different projects available from the EmployeeSalary table.
Ans. While referring to the EmployeeSalary table, we can see that this table contains project values corresponding to each employee, or we can say that we will have duplicate project values while selecting Project values from this table.

So, we will use the distinct clause to get the unique values of the Project.

SELECT DISTINCT(Project)
FROM EmployeeSalary;



Ques.3. Write an SQL query to fetch the count of employees working in project ‘P1’.
Ans. Here, we would be using aggregate function count() with the SQL where clause-

SELECT COUNT(*) 
FROM EmployeeSalary 
WHERE Project = 'P1';



Ques.4. Write an SQL query to find the maximum, minimum, and average salary of the employees.
Ans. We can use the aggregate function of SQL to fetch the max, min, and average values-

SELECT Max(Salary), 
Min(Salary), 
AVG(Salary) 
FROM EmployeeSalary;



Ques.5. Write an SQL query to find the employee id whose salary lies in the range of 9000 and 15000.
Ans. Here, we can use the ‘Between’ operator with a where clause.

SELECT EmpId, Salary
FROM EmployeeSalary
WHERE Salary BETWEEN 9000 AND 15000;



Ques.6. Write an SQL query to fetch those employees who live in Toronto and work under the manager with ManagerId – 321.
Ans. Since we have to satisfy both the conditions – employees living in ‘Toronto’ and working in Project ‘P2’. So, we will use AND operator here-

SELECT EmpId, City, ManagerId
FROM EmployeeDetails
WHERE City='Toronto' AND ManagerId='321';



Ques.7. Write an SQL query to fetch all the employees who either live in California or work under a manager with ManagerId – 321.
Ans. This interview question requires us to satisfy either of the conditions – employees living in ‘California’ and working under Manager with ManagerId – 321. So, we will use the OR operator here-

SELECT EmpId, City, ManagerId
FROM EmployeeDetails
WHERE City='California' OR ManagerId='321';



Ques.8. Write an SQL query to fetch all those employees who work on Projects other than P1.
Ans. Here, we can use the NOT operator to fetch the rows which are not satisfying the given condition.

SELECT EmpId
FROM EmployeeSalary
WHERE NOT Project='P1';


Or using the ‘not equal to’ operator-

SELECT EmpId
FROM EmployeeSalary
WHERE Project <> 'P1';

For the difference between NOT and <> SQL operators, check this link – Difference between the NOT and != operators.



Ques.9. Write an SQL query to display the total salary of each employee adding the Salary with Variable value.
Ans. Here, we can simply use the ‘+’ operator in SQL.

SELECT EmpId,
Salary+Variable as TotalSalary 
FROM EmployeeSalary;



Ques.10. Write an SQL query to fetch the employees whose name begins with any two characters, followed by a text “hn” and ends with any sequence of characters.
Ans. For this question, we can create an SQL query using like operator with ‘_’ and ‘%’ wild card characters, where ‘_’ matches a single character and ‘%’ matches ‘0 or multiple characters.

SELECT FullName
FROM EmployeeDetails
WHERE FullName LIKE ‘__hn%’;



Ques.11. Write an SQL query to fetch all the EmpIds which are present in either of the tables – ‘EmployeeDetails’ and ‘EmployeeSalary’.
Ans. In order to get unique employee ids from both tables, we can use the Union clause which can combine the results of the two SQL queries and return unique rows.

SELECT EmpId FROM EmployeeDetails
UNION 
SELECT EmpId FROM EmployeeSalary;



Ques.12. Write an SQL query to fetch common records between two tables.
Ans. SQL Server – Using INTERSECT operator-

SELECT * FROM EmployeeSalary
INTERSECT
SELECT * FROM ManagerSalary;


MySQL – Since MySQL doesn’t have INTERSECT operator so we can use the subquery-

SELECT *
FROM EmployeeSalary
WHERE EmpId IN 
(SELECT EmpId from ManagerSalary);


Ques.13. Write an SQL query to fetch records that are present in one table but not in another table.
Ans. SQL Server – Using MINUS- operator-

SELECT * FROM EmployeeSalary
MINUS
SELECT * FROM ManagerSalary;


MySQL – Since MySQL doesn’t have a MINUS operator so we can use LEFT join-

SELECT EmployeeSalary.*
FROM EmployeeSalary
LEFT JOIN
ManagerSalary USING (EmpId)
WHERE ManagerSalary.EmpId IS NULL;



Ques.14. Write an SQL query to fetch the EmpIds that are present in both the tables –   ‘EmployeeDetails’ and ‘EmployeeSalary.
Ans. Using subquery-

SELECT EmpId FROM 
EmployeeDetails 
where EmpId IN 
(SELECT EmpId FROM EmployeeSalary);



Ques.15. Write an SQL query to fetch the EmpIds that are present in EmployeeDetails but not in EmployeeSalary.
Ans. Using subquery-

SELECT EmpId FROM 
EmployeeDetails 
where EmpId Not IN 
(SELECT EmpId FROM EmployeeSalary);



Ques.16. Write an SQL query to fetch the employee’s full names and replace the space with ‘-’.
Ans. Using the ‘Replace’ function-

SELECT REPLACE(FullName, ' ', '-') 
FROM EmployeeDetails;



Ques.17. Write an SQL query to fetch the position of a given character(s) in a field.
Ans. Using the ‘Instr’ function-

SELECT INSTR(FullName, 'Snow')
FROM EmployeeDetails;



Ques.18. Write an SQL query to display both the EmpId and ManagerId together.
Ans. Here we can use the CONCAT command.

SELECT CONCAT(EmpId, ManagerId) as NewId
FROM EmployeeDetails;



Ques.19. Write a query to fetch only the first name(string before space) from the FullName column of the EmployeeDetails table.
Ans. In this question, we are required to first fetch the location of the space character in the FullName field and then extract the first name out of the FullName field.

For finding the location we will use the LOCATE method in MySQL and CHARINDEX in SQL SERVER and for fetching the string before space, we will use the SUBSTRING OR MID method.

MySQL – using MID

SELECT MID(FullName, 1, LOCATE(' ',FullName)) 
FROM EmployeeDetails;


SQL Server – using SUBSTRING

SELECT SUBSTRING(FullName, 1, CHARINDEX(' ',FullName)) 
FROM EmployeeDetails;



Ques.20. Write an SQL query to uppercase the name of the employee and lowercase the city values.
Ans. We can use SQL Upper and Lower functions to achieve the intended results.

SELECT UPPER(FullName), LOWER(City) 
FROM EmployeeDetails;



Ques.21. Write an SQL query to find the count of the total occurrences of a particular character – ‘n’ in the FullName field.
Ans. Here, we can use the ‘Length’ function. We can subtract the total length of the FullName field from the length of the FullName after replacing the character – ‘n’.

SELECT FullName, 
LENGTH(FullName) - LENGTH(REPLACE(FullName, 'n', ''))
FROM EmployeeDetails;



Ques.22. Write an SQL query to update the employee names by removing leading and trailing spaces.
Ans. Using the ‘Update’ command with the ‘LTRIM’ and ‘RTRIM’ functions.

UPDATE EmployeeDetails 
SET FullName = LTRIM(RTRIM(FullName));


Ques.23. Fetch all the employees who are not working on any project.
Ans. This is one of the very basic interview questions in which the interviewer wants to see if the person knows about the commonly used – Is NULL operator.

SELECT EmpId 
FROM EmployeeSalary 
WHERE Project IS NULL;



Ques.24. Write an SQL query to fetch employee names having a salary greater than or equal to 5000 and less than or equal to 10000.
Ans. Here, we will use BETWEEN in the ‘where’ clause to return the EmpId of the employees with salary satisfying the required criteria and then use it as a subquery to find the fullName of the employee from the EmployeeDetails table.

SELECT FullName 
FROM EmployeeDetails 
WHERE EmpId IN 
(SELECT EmpId FROM EmployeeSalary 
WHERE Salary BETWEEN 5000 AND 10000);



Ques.25. Write an SQL query to find the current date-time.
Ans. MySQL-

SELECT NOW();


SQL Server-

SELECT getdate();


Oracle-

SELECT SYSDATE FROM DUAL;


Ques.26. Write an SQL query to fetch all the Employee details from the EmployeeDetails table who joined in the Year 2020.
Ans. Using BETWEEN for the date range ’01-01-2020′ AND ’31-12-2020′-

SELECT * FROM EmployeeDetails
WHERE DateOfJoining BETWEEN '2020/01/01'
AND '2020/12/31';


Also, we can extract the year part from the joining date (using YEAR in MySQL)-

SELECT * FROM EmployeeDetails 
WHERE YEAR(DateOfJoining) = '2020';


Ques.27. Write an SQL query to fetch all employee records from the EmployeeDetails table who have a salary record in the EmployeeSalary table.
Ans. Using ‘Exists’-

SELECT * FROM EmployeeDetails E
WHERE EXISTS
(SELECT * FROM EmployeeSalary S 
WHERE  E.EmpId = S.EmpId);


Ques.28. Write an SQL query to fetch the project-wise count of employees sorted by project’s count in descending order.
Ans. The query has two requirements – first to fetch the project-wise count and then to sort the result by that count.

For project-wise count, we will be using the GROUP BY clause and for sorting, we will use the ORDER BY clause on the alias of the project count.

SELECT Project, count(EmpId) EmpProjectCount
FROM EmployeeSalary
GROUP BY Project
ORDER BY EmpProjectCount DESC;


Ques.29. Write a query to fetch employee names and salary records. Display the employee details even if the salary record is not present for the employee.
Ans. This is again one of the very common interview questions in which the interviewer just wants to check the basic knowledge of SQL JOINS.

Here, we can use the left join with the EmployeeDetail table on the left side of the EmployeeSalary t

able.

SELECT E.FullName, S.Salary 
FROM EmployeeDetails E 
LEFT JOIN 
EmployeeSalary S
ON E.EmpId = S.EmpId;



Ques.30. Write an SQL query to join 3 tables.
Ans. Considering 3 tables TableA, TableB, and TableC, we can use 2 joins clauses like below-
sql query interview questions

SELECT column1, column2
FROM TableA
JOIN TableB ON TableA.Column3 = TableB.Column3
JOIN TableC ON TableA.Column4 = TableC.Column4;

    For more questions on SQL Joins, you can also check our top SQL Joins Interview Questions.

Powered By
VDO.AI










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
