### Normalization:

Normalization is the process of reorganizing data in a database so that it meets two basic requirements:  
1) **No redundancy of data:** All data is stored in only one place.  
2) **Logical data dependencies:** All related data items are stored together.  

**Need for normalization:**  
1) It eliminates redundant data.  
2) It reduces chances of data error.  
3) It is important because it allows the database to take up less disk space.  
4) It helps increase performance.  
5) It improves data integrity and consistency.

---

### **Redundancy and Its Problems**  
- **Redundancy** is at the root of several problems associated with relational schemas.  

**Problems caused by redundancy:**  
1) **Redundant storage:** Some information is stored repeatedly.  
2) **Update anomalies:** If one copy of such repeated data is updated, inconsistencies are created unless all other copies are similarly updated.  
3) **Insertion anomalies:** When inserting new records, repeated information is added to the schema.  
4) **Deletion anomalies:** Deleting a record can also delete associated important information, leading to data loss.

---

### **Explanation of Anomalies Using Example**

1) **Redundant storage:**  
   Information about `DeptID`, `DeptName`, and `DeptLoc` is repeated in the table.

2) **Update anomalies:**  
   If the `DeptLoc` for `DeptID 101` is changed from Pune to Chennai, this creates inconsistencies since multiple records will have to be updated.  

3) **Insertion anomalies:**  
   If we want to add a new tuple, such as `(5, EEE, 50000)` for `DeptID 101`, the repeated data for `(101, XYZ, Pune)` will occur.

4) **Deletion anomalies:**  
   If we delete a record with `EmpID 4`, information about `DeptID 102`, `DeptName PQR`, and `DeptLoc Mumbai` will also be deleted. This causes data loss.

### **2NF (Second Normal Form)***
Definition:
A table is in 2NF if:
- It is in 1NF (data is atomic, no repeating groups).
- It has no partial dependencies (all non-prime attributes depend on the entire primary key, not just a part of it).

Converting to 2NF:

Step 1: Identify Partial Dependencies
EmpName depends on EmpID.
ProjectName depends on ProjectID.
HoursWorked depends on the full composite key (EmpID, ProjectID).

Step 2: Split the Table to Remove Partial Dependencies
Employee Table: </br>
EmpID	EmpName  </br>
101	Alice </br>
102	Bob </br>
103	Charlie </br>

Project Table: </br>
ProjectID	ProjectName </br>
P1	Alpha Project </br>
P2	Beta Project </br>
P3	Gamma Project </br>

Employee_Project Table (Bridge Table): </br>
EmpID	ProjectID	HoursWorked </br>
101	P1	20 </br>
101	P2	15 </br>
102	P1	30 </br>
103	P3	25 </br>

Benefits of 2NF: </br>
- No partial dependencies: </br>
EmpName is dependent only on EmpID. </br>
ProjectName is dependent only on ProjectID. </br>
- Reduced redundancy: </br>
Employee and project details are stored only once. </br>
- Improved consistency:
Updates to employee or project names happen in one place, avoiding anomalies.

### **3NF (Third Normal Form) Normalization:**
Definition: A table is in Third Normal Form (3NF) if:
It is in Second Normal Form (2NF).
It has no transitive dependencies.

Why Normalize to 3NF?
To remove transitive dependencies and ensure that non-prime attributes have a direct relationship with the primary key, reducing redundancy and improving data integrity.

Example:
Table in 2NF (but not in 3NF): </br>
Student Table </br>
StudentID	StudentName	DeptID	DeptName	DeptHead </br>
1	Alice	D1	Science	Dr. Smith </br>
2	Bob	D2	Arts	Dr. Taylor </br>
3	Charlie	D1	Science	Dr. Smith </br>
Primary Key: StudentID </br>

Non-prime attributes: StudentName, DeptID, DeptName, DeptHead. </br>

Issues:
- Transitive Dependency:
DeptName and DeptHead depend on DeptID, which in turn depends on StudentID.
StudentID → DeptID → DeptName, DeptHead.
- Redundancy:
DeptName and DeptHead repeat for the same DeptID.

Converting to 3NF
- Step 1: Identify Transitive Dependencies
DeptName and DeptHead depend on DeptID, not directly on StudentID.
- Step 2: Split the Table to Remove Transitive Dependencies
Student Table: </br>
StudentID	StudentName	DeptID </br>
1	Alice	D1 </br>
2	Bob	D2 </br>
3	Charlie	D1 </br>

Department Table: </br>
DeptID	DeptName	DeptHead </br>
D1	Science	Dr. Smith </br>
D2	Arts	Dr. Taylor </br>

Benefits of 3NF:
- No transitive dependency: Non-prime attributes (DeptName, DeptHead) now depend only on the primary key of their respective table (DeptID in Department table).
- Reduced redundancy: Department details are stored only once in the Department table.
- Improved consistency: Updating department information affects only the Department table.
