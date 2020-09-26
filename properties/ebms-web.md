---
sort: 1
---

# ebms-web.properties

```properties
#SSL
https.verifyHostnames=false

#Security
keystore.path=${catalina.base}/conf/keystore.jks
keystore.password=password

truststore.path=${catalina.base}/conf/truststore.jks
truststore.password=password

signature.keystore.path=${catalina.base}/conf/keystore.jks
signature.keystore.password=password

#JDBC
ebms.jdbc.username=ebms
ebms.jdbc.password=<password>

#MSSQL
#ebms.jdbc.driverClassName=com.microsoft.sqlserver.jdbc.SQLServerDriver
#ebms.jdbc.url=jdbc:sqlserver://localhost:1433;databaseName=ebms;
#ebms.pool.preferredTestQuery=select 1

#MySQL
#ebms.jdbc.driverClassName=com.mysql.jdbc.Driver
#ebms.jdbc.url=jdbc:mysql://localhost:3306/ebms
#ebms.pool.preferredTestQuery=select 1

#Oracle
#ebms.jdbc.driverClassName=oracle.jdbc.OracleDriver
#ebms.jdbc.url=jdbc\:oracle\:thin\:@//localhost\:1521/ebms
#ebms.pool.preferredTestQuery=select 1 from dual

#Postgres
#ebms.jdbc.driverClassName=org.postgresql.Driver
#ebms.jdbc.url=jdbc:postgresql://localhost:5432/ebms
#ebms.pool.preferredTestQuery=select 1
```
