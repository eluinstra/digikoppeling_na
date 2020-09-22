---
sort: 3
---

# gb-web.properties

```properties
gb.fileShare=/tmp/gb
gb.workingDir=/tmp/workingDir

# SSL
https.verifyHostnames=true

client.keystore.path=keystore.jks
client.keystore.password=password

truststore.path=keystore.jks
truststore.password=password

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
