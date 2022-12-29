# SQL Queries

$$\color{purple}{SQL \ Queries}$$

<button>
:link:[Home](all-file-links.md)     
</button>


<a name="top"></a>
 [Go To Bottom](#bottom)
 
 
# Topics

   [Go To Top](#top)
   
   [0 SQL Interviews Questions](#sql_interviews_questions)

   [30 SQL Interviews Questions](#sql_interviews_questions_30)







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
