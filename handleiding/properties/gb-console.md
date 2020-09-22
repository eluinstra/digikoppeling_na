---
sort: 4
---

# gb-console.properties

```properties
service.gb.url=http://localhost:8088/gb-adapter-web/gb
service.ebms.url=http://localhost:8088/ebms-adapter-web/service/ebms

upload.tenantId=na
upload.cpaId=cpa_1_upload
upload.partyId=urn:na:id:1

gb.fileShare=/tmp/gb
gb.uploadUrl=https://gb-acpt.nationaalarchief.nl/gb/tenant_NLHaNA/upload/
gb.maxSize=0
gb.compression=NONE

#JDBC
gb.jdbc.username=ebms
gb.jdbc.password=<password>

#MSSQL
#gb.jdbc.driverClassName=com.microsoft.sqlserver.jdbc.SQLServerDriver
#gb.jdbc.url=jdbc:sqlserver://localhost:1433;databaseName=ebms;
#gb.pool.preferredTestQuery=select 1

#MySQL
#gb.jdbc.driverClassName=com.mysql.jdbc.Driver
#gb.jdbc.url=jdbc:mysql://localhost:3306/ebms
#gb.pool.preferredTestQuery=select 1

#Oracle
#gb.jdbc.driverClassName=oracle.jdbc.OracleDriver
#gb.jdbc.url=jdbc\:oracle\:thin\:@//localhost\:1521/ebms
#gb.pool.preferredTestQuery=select 1 from dual

#Postgres
#gb.jdbc.driverClassName=org.postgresql.Driver
#gb.jdbc.url=jdbc:postgresql://localhost:5432/ebms
#gb.pool.preferredTestQuery=select 1
```
