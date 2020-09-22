---
sort: 5
---

# Installatie Grote Berichten adapter

Dit hoofdstuk beschrijft de installatie van de open source Grote Berichten adapter. Deze handleiding gaat uit van het gebruik van de web versie van de Grote Berichten adapter voor Tomcat.

## Benodigde software
Zie [Benodigde software]({{ site.baseurl }}/handleiding/installatie-ebms.html#benodigde-software)

Download de volgende software
- [gb-adapter-web-2.4.4.war](https://bitbucket.org/eluinstra/gb-adapter-web/downloads/gb-adapter-web-2.4.4.war) - bevat de Grote Berichten adapter voor tomcat

## Configuratie Tomcat
Zie [Configuratie Tomcat]({{ site.baseurl }}/handleiding/installatie-ebms.html#configuratie-tomcat)

## Tomcat Grote Berichten adapter
Voor het installeren van de Grote Berichten adapter moet er eerst een keystore worden gegenereerd met daarin de Key en bijbehorende Certificaten van de partner. Ook is er een truststore nodig met daarin de Certificaten van het Nationaal Archief. De truststore wordt samen met de software aangeleverd door het Nationaal Archief, of is zelf te genereren mbv. de juiste certificaten per omgeving (zie [Grote Berichten Service Omgevingen]({{ site.baseurl }}/handleiding/technische-beschrijving-gb.html#grote-berichten-service-omgevingen)). Vervolgens kan de configuratie worden aangemaakt en kan de Grote Berichten adapter worden geïnstalleerd.

### Genereren Keystore
Zie [Genereren Keystore]({{ site.baseurl }}/handleiding/installatie-ebms.html#genereren-keystore)

### Configureren gb-web.properties
De applicatie maakt gebruik van properties. De default properties kunnen worden overridden. De locatie van de override properties file is `<catalina.home>/conf/gb-web.properties`  
Hieronder volgt een overzicht van de belangrijkste properties per category die zouden kunnen worden overridden. [gb-web.properties]({{ site.baseurl }}{% link handleiding/properties/gb-web.md %}) bevat een voorbeeld van het `gb-web.properties` bestand.

![image](/assets/images/gb-web.png)

#### Common
De applicatie biedt de volgende properties voor Common configuratie
-	`gb.fileShare`
-	`gb.workingDir`

`gb.fileShare` bevat het pad naar de directory waarin de bestanden worden aangeboden aan de Grote Berichten adapter.  
`gb.workingDir` bevat het pad naar de wek directory van de Grote Berichten adapter.  

#### SSL
De applicatie biedt de volgende properties voor SSL configuratie
-	`https.verifyHostnames`
-	`client.keystore.path`
-	`client.keystore.password`
-	`truststore.path`
-	`truststore.password` 

`https.verifyHostnames` (`true`\|`false`) bepaalt of de client de hostname moet verifieren.  

`client.keystore.path` bevat het pad naar de SSL keystore.  
`client.keystore.password` bevat het wachtwoord van de SSL keystore. Het wachtwoord van de key dient gelijk te zijn aan het wachtwoord van de SSL keystore.  

`truststore.path` bevat het pad naar de SSL truststore. De truststore dient de ca certificate chain te bevatten.  
`truststore.password` bevat het wachtwoord van de SSL truststore.  

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

#### Routeren via proxy server

Het is ook mogelijk om uitgaand verkeerd te routeren via een proxy server.

![image](/assets/images/gb-web-rproxy.png)

Voeg hiervoor de volgende properties toe aan gb-web.properties (zie Configureren gb-web.properties):

`http.proxyHost` bevat het ipadres of de hostname van de proxy server.  
`http.proxyPort` bevat de port van de proxy server.  
`http.nonProxyHosts` bevat een comma separated string met ipadressen en/of hostnames van de hosts die niet via de proxy server moeten worden gerouteerd. De default waarde is 127.0.0.1,localhost.  
`http.proxyUser` bevat de gebruikersnaam voor de proxy server.  
`http.proxyPassword` bevat het wachtwoord voor de proxy server.  

### Installeren Grote Berichten adapter

Voer de volgende acties uit voor het installeren van de Grote Berichten adapter

#### Linux
```sh
chown tomcat:tomcat gb-web.properties keystore.jks truststore.jks
cp gb-web.properties keystore.jks truststore.jks $TOMCAT_HOME/conf/
cp gb-adapter-2.4.4.1.war $TOMCAT_HOME/webapps/gb-adapter.war
```

#### Windows
```sh
copy gb-web.properties %TOMCAT_HOME%\conf\
copy keystore.jks %TOMCAT_HOME%\conf\
copy truststore.jks %TOMCAT_HOME%\conf\
copy gb-adapter-2.4.4.1.war %TOMCAT_HOME%\webapps\gb-adapter.war
```

De gb-adapter soap interface is vervolgens bereikbaar op [http://localhost:8080/gb-adapter-web/gb](http://localhost:8080/gb-adapter-web/gb).
