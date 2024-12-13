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
