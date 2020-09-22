---
sort: 6
---

# Installatie Grote Berichten console

Dit hoofdstuk beschrijft de installatie van de open source Grote Berichten console. Deze handleiding gaat uit van het gebruik van de web versie van de Grote Berichten console voor Tomcat.

## Benodigde software
Zie [Benodigde software]({{ site.baseurl }}/handleiding/installatie-ebms.html#benodigde-software)

Download de volgende software
- [gb-console-web-2.4.4.0.war](https://bitbucket.org/eluinstra/gb-console-web/downloads/gb-console-web-2.4.4.0.war) - bevat de Grote Berichten console voor tomcat.

## Configuratie Tomcat
Zie [Configuratie Tomcat]({{ site.baseurl }}/handleiding/installatie-ebms.html#configuratie-tomcat)

### Configureren gb-console.properties
De applicatie maakt gebruik van properties. De default properties kunnen worden overridden. De locatie van de override properties file is `<catalina.home>/conf/gb-console.properties`  
Hieronder volgt een overzicht van de belangrijkste properties per catogory die zouden kunnen worden overridden. [gb-console.properties]({{ site.baseurl }}{% link handleiding/properties/gb-console.md %}) bevat een voorbeeld van het `gb-console.properties` bestand.

![image]({{ site.baseurl }}/assets/images/gb-web.png)

#### Grote berichten adapter properties
De applicatie biedt de volgende properties voor Grote Berichten interface configuratie
-	`service.gb.url`
-	`gb.fileShare`
-	`gb.uploadUrl`
-	`gb.maxSize`
-	`gb.compression`

`service.gb.url` bevat de url naar de Grote Berichten adapter.  
`gb.fileShare` bevat het pad naar de directory waarin de bestanden worden aangeboden aan de Grote Berichten console. NB: de waarde is gelijk aan de waarde van de property.  
`gb.fileShare` van de Grote Berichten adapter (zie Common).  
`gb.uploadUrl` bevat de url naar de upload locatie op de Grote Berichten server (zie Grote Berichten Service Omgevingen, https://`<servernaam>`/gb/`<klantId>`/upload) die de Grote Berichten adapter gebruikt om bestanden naar toe te versturen.  
`gb.maxSize` bevat de max file size in bytes die de Grote Berichten adapter gebruikt om bestanden te versturen. De waarde 0 betekent geen max file size.  
`gb.compression` bevat de compressie methode die de Grote Berichten adapter gebruikt om bestanden te versturen (`NONE`\|`ZIP4J`).  

#### EbMS adapter properties
De applicatie biedt de volgende properties voor interface configuratie
-	`service.ebms.url`
-	`upload.tenantId`
-	`upload.cpaId`
-	`upload.partyId`
-	`upload.role`

`service.ebms.url` bevat de url naar de EbMS adapter.  
`upload.tenantId` bevat de klantId/ISIL code van de klant.  
`upload.cpaId` bevat de cpaId van de uploadExportBestand EbMS service.  
`upload.partyId` bevat de partyId van de klant in het volgende formaat urn:na:oin:`<OIN>`.  
`upload.role` bevat de role van de klant.  

#### JDBC
De applicatie biedt de volgende properties voor JDBC configuratie
-	`gb.jdbc.driverClassName`
-	`gb.jdbc.url`
-	`gb.jdbc.username`
-	`gb.jdbc.password`

`gb.jdbc.driverClassName` bevat de database driver class name. De class name hangt af van de gebruikte database.  
`gb.jdbc.url` bevat de connectie string voor de Grote Berichten database. Het formaat van de connectie string hangt af van de gebruikte database.  
`gb.jdbc.username` bevat de gebruikersnaam voor de Grote Berichten database.  
`gb.jdbc.password` bevat het wachtwoord voor de Grote Berichten database.  

Hierna volgt de beschrijving van de driver class names en connectie string formaten voor de verschillende databases

##### MSSQL
```properties
gb.jdbc.driverClassName=com.microsoft.sqlserver.jdbc.SQLServerDriver
gb.jdbc.url=jdbc:sqlserver://<host>:<port>;databaseName=<dbname>;
```

##### MySQL
```properties
gb.jdbc.driverClassName=com.mysql.jdbc.Driver
gb.jdbc.url=jdbc:mysql://<host>:<port>/<dbname>
```

##### Oracle
```properties
gb.jdbc.driverClassName=oracle.jdbc.OracleDriver
gb.jdbc.url=jdbc:oracle:thin:@<host>:<port>:<dbname>
```

##### PostgreSQL
```properties
gb.jdbc.driverClassName=org.postgresql.Driver
gb.jdbc.url=jdbc:postgresql://<host>:<port>/<dbname>
```

### Installeren Grote Berichten console
Voer de volgende acties uit voor het installeren van de Grote Berichten adapter

#### Linux
```sh
chown tomcat:tomcat gb-console.properties
cp gb-console.properties $TOMCAT_HOME/conf/
cp gb-console-2.4.4.1.war $TOMCAT_HOME/webapps/gb-console.war
```

#### Windows
```powershell
copy gb-console.properties %TOMCAT_HOME%\conf\
copy gb-console-2.4.4.1.war %TOMCAT_HOME%\webapps\gb-console.war
```