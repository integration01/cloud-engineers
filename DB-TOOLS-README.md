# Using Database-Related Tools and Services

This page covers the following:
- Using Autonomous Recovery Service
- Using SQL Worksheet
- Using Database Management

All of these tools and services are available in our tenancy, but should be used with caution.  There are limits we must respect, so please follow the rules here and remember to terminate resources that are not needed.

## Autonomous Recovery Service
Databases within shared ExaCS / ADB-D are enabled for use within ASR.  This can be enabled when the database is created or after the fact.  Once enabled, check both the Protected Databases screen and the Backups screen for your DB to ensure you are getting valid backups.

### ASR Example
![ASR Success](images/ASR-Successful.png)
![ASR Protected DB](images/ASR-Protected-DB.png)

## SQL Worksheet / DB Tools
The tenancy now allows for the use of SQL Worksheet.  You can create a connection within your own compartment.  Steps:
1) Create a secret in the cloud-engineering-vault for the SYS password you used when creating your database
2) Create a Connection under DB Tools using this secret (connect as SYSDBA).  Select the Private Endpoint called `EXACSPRI` within the `ExaCS` compartment.
   a) The wallet screen is optional
4) Enter SQL Worksheet and ensure your connection is selected

### SQL Worksheet Example
![SQLW Conn](images/SQLWorksheet-Connection1.png)
![SQLW Conn](images/SQLWorksheet-Connection2.png)
![SQLW Conn](images/SQLWorksheet-Enabled.png)

## Database Management
Databases on ExaCS are eligible for both Basic and Full management using Database Management.  Be judicious about using full management.  You can switch back and forth between versions and enabled/disabled.  Steps:
1) Enable the DBSNMP user in your database.  You can do this via SQL Worksheet.  You can use the same password as sys or a new one 
```sql
ALTER USER dbsnmp ACCOUNT UNLOCK;
ALTER USER dbsnmp IDENTIFIED BY xxxx;
GRANT CREATE PROCEDURE to DBSNMP;
GRANT SELECT ANY DICTIONARY, SELECT_CATALOG_ROLE to DBSNMP;
GRANT ALTER SYSTEM to DBSNMP;
GRANT ADVISOR to DBSNMP;
GRANT EXECUTE ON DBMS_WORKLOAD_REPOSITORY to DBSNMP;
```
2) If you chose a new password for DBSNMP, create another secret in the cloud-engineering-vault for the DBSNMP password you used above
3) Follow the Database Management enablement wizard from your database (do not select "add policy" - this is done already)
4) Choose the private endpoint called `ExaCS_PE` within the ExaCs compartment
5) Choose Full or Basic

### Database Management Example
![DBM Enable](images/DBM-Enable1.png)
![DBM Enable](images/DBM-Enable2.png)
If you can enabled full management and ran the DBSNMP grants above, you will see the Performance Hub:
![DBM Enable](images/DBM-PerfHub.png)
