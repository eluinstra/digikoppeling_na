---
sort: 3
---

# Installatie EbMS adapter

Dit hoofdstuk beschrijft de installatie van de open source EbMS adapter. Deze handleiding gaat uit van het gebruik van de web versie van de EbMS adapter voor Tomcat.

## Benodigde software

Installeer de volgende software
- Java 7 of hoger
- Java Cryptography Extension (JCE) Unlimited Strength
- Tomcat 7 of hoger

Download de volgende software
- [ebms-adapter-web-2.13.6.war](https://sourceforge.net/projects/muleebmsadapter/files/ebms/ebms-adapter-web/ebms-adapter-web-2.13.6.war/download) - bevat de EbMS adapter voor tomcat
- [ebms-admin-2.13.6.jar](https://sourceforge.net/projects/javaebmsadmin/files/ebms-admin-2.13.6.jar/download) - bevat de EbMS Admin Console
- [JDBC driver](#jdbc) voor de database

## Configuratie Proxy server

De proxy server dient SSL te ondersteunen waarbij de SSL key en certificaten van de partner
en de SSL certificaten van het Nationaal Archief ten behoeve van client authentication zijn geconfigureerd en de volgende SSL settings zijn geconfigureerd:
- SSL Protocol: TLSv1.2
- SSL Cipher Suite: AES128-SHA256,AES256-SHA256,AES256-SHA,AES128-SHA
- Require client authentication

Verder moet de proxy server het externe verkeer routeren naar de EbMS adapter. Zie [Installeren EbMS adapter](#installeren-ebms-adapter) voor de url van de EbMS interface.

## Configuratie Tomcat

Zet de volgende Catalina opties
```sh
export CATALINA_OPTS="-Dhttps.protocols=TLSv1.2 -Dhttps.cipherSuites=TLS_RSA_WITH_AES_256_CBC_SHA256,TLS_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_256_CBC_SHA,TLS_RSA_WITH_AES_128_CBC_SHA -Dorg.apache.commons.logging.LogFactory=org.apache.commons.logging.impl.LogFactoryImpl -Djavax.net.ssl.trustStore="
```

## Tomcat EbMS adapter
Voor het installeren van de EbMS adapter moet er eerst een keystore worden gegenereerd met daarin de Key en bijbehorende Certificaten van de (keten)partner. Ook is er een truststore nodig met daarin de Certificaten van het Nationaal Archief. De truststore wordt samen met de software aangeleverd door het Nationaal Archief, of is zelf te genereren m.b.v. de juiste certificaten per omgeving (zie [EbMS Omgevingen]({{ site.baseurl }}/handleiding/technische-beschrijving-ebms#ebms-omgevingen)). Vervolgens kan de configuratie worden aangemaakt en kan de EbMS adapter worden geïnstalleerd.

### Genereren Keystore

Als de certificaten door de CA zijn aangeleverd als pkcs7 bestand `<organisatie>.p7c`, exporteer de certificaten als volgt
```sh
openssl pkcs7 -in <organisatie>.p7c -print_certs -out certificates.pem

cp certificates.pem certificate.pem
vi certificate.pem
# only keep first certificate

cp certificates.pem ca.pem
vi ca.pem
# only remove first certificate
```

Creeer pkcs12 keystore
```sh
openssl pkcs12 -export -out keystore.p12 -inkey [organisatie].key -in certificate.pem -certfile ca.pem
```

Creeer jks keystore
```sh
keytool -importkeystore -srcstoretype pkcs12 -srckeystore keystore.p12 -deststoretype JKS -destkeystore keystore.jks
```

### Configureren ebms-web.properties
De applicatie maakt gebruik van properties. De default properties kunnen worden overridden. De locatie van de override properties file is `<catalina.home>/conf/ebms-web.properties`  
Hieronder volgt een overzicht van de belangrijkste properties per catogory die zouden kunnen worden overridden. [ebms-web.properties]({{ site.baseurl }}{% link properties/ebms-web.md %}) bevat een voorbeeld van het `ebms-web.properties` bestand.

![image]({{ site.baseurl }}/assets/images/ebms-web.png)

#### SSL
De applicatie biedt de volgende properties voor SSL configuratie
-	`https.verifyHostnames`

`https.verifyHostnames` (`true`\|`false`) bepaalt of de client de hostname moet verifieren.

#### Security
De applicatie biedt de volgende properties voor SSL & EbMS Signature configuratie
-	`keystore.path`
-	`keystore.password`
-	`truststore.path`
-	`truststore.password`
-	`signature.keystore.path`
-	`signature.keystore.password`

`keystore.path` bevat het pad naar de SSL keystore.  
`keystore.password` bevat het wachtwoord van de SSL keystore. Het wachtwoord van de key dient gelijk te zijn aan het wachtwoord van de SSL keystore.

`truststore.path` bevat het pad naar de SSL en EbMS Signature truststore. De truststore dient de ca certificate chain te bevatten.  
`truststore.password` bevat het wachtwoord van de SSL en EbMS Signature truststore.

`signature.keystore.path` bevat het pad naar de EbMS Signature keystore.  
`signature.keystore.password` bevat het wachtwoord van de EbMS Signature keystore.

#### JDBC
De applicatie biedt de volgende properties voor JDBC configuratie
-	`ebms.jdbc.driverClassName`
-	`ebms.jdbc.url`
-	`ebms.jdbc.username`
-	`ebms.jdbc.password`

`jdbc.driverClassName` bevat de database driver class name. De class name hangt af van de gebruikte database.  
`jdbc.url` bevat de connectie string voor de EbMS database. Het formaat van de connectie string hangt af van de gebruikte database.  
`jdbc.username` bevat de gebruikersnaam voor de EbMS database.  
`jdbc.password` bevat het wachtwoord voor de EbMS database.  

Hierna volgt de beschrijving van de driver class names en connectie string formaten voor de verschillende databases

##### MSSQL
```properties
ebms.jdbc.driverClassName=com.microsoft.sqlserver.jdbc.SQLServerDriver
ebms.jdbc.url=jdbc:sqlserver://<host>:<port>;databaseName=<dbname>;
```

Download JDBC driver [hier](https://docs.microsoft.com/en-us/sql/connect/jdbc/download-microsoft-jdbc-driver-for-sql-server)

##### MySQL
```properties
ebms.jdbc.driverClassName=com.mysql.jdbc.Driver
ebms.jdbc.url=jdbc:mysql://<host>:<port>/<dbname>
```

Download JDBC driver [hier](https://dev.mysql.com/downloads/connector/j/)  

##### Oracle
```properties
ebms.jdbc.driverClassName=oracle.jdbc.OracleDriver
ebms.jdbc.url=jdbc:oracle:thin:@<host>:<port>:<dbname>
```

Download JDBC driver [hier](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html)

##### PostgreSQL
```properties
ebms.jdbc.driverClassName=org.postgresql.Driver
ebms.jdbc.url=jdbc:postgresql://<host>:<port>/<dbname>
```

Download JDBC driver [hier](https://jdbc.postgresql.org/download.html)  

#### Routeren via proxy server
Het is ook mogelijk om uitgaand verkeerd te routeren via een proxy server.

![image]({{ site.baseurl }}/assets/images/ebms-web-rproxy.png)

Voeg hiervoor de volgende properties toe aan `ebms-web.properties` (zie [Configureren ebms-web.properties](#configureren-ebms-webproperties)):

`http.proxy.host` bevat het ipadres of de hostname van de proxy server.  
`http.proxy.port` bevat de port van de proxy server.  
`http.proxy.nonProxyHosts` bevat een comma separated string met ipadressen en/of hostnames van de hosts die niet via de proxy server moeten worden gerouteerd. De default waarde is 127.0.0.1,localhost.  
`http.proxy.username` bevat de gebruikersnaam voor de proxy server.  
`http.proxy.password` bevat het wachtwoord voor de proxy server.  

### Installeren EbMS adapter

Voer de volgende acties uit voor het installeren van de EbMS adapter

#### Linux
```sh
chown tomcat:tomcat ebms-web.properties keystore.jks truststore.jks <jdbc-driver.jar>
cp <jdbc-driver.jar> $TOMCAT_HOME/lib/
cp ebms-web.properties keystore.jks truststore.jks $TOMCAT_HOME/conf/
cp ebms-adapter-2.13.6.war $TOMCAT_HOME/webapps/ebms-adapter.war
```

#### Windows
```powershell
copy <jdbc-driver.jar> %TOMCAT_HOME%\lib\
copy ebms-web.properties %TOMCAT_HOME%\conf\
copy keystore.jks %TOMCAT_HOME%\conf\
copy truststore.jks %TOMCAT_HOME%\conf\
copy ebms-adapter-2.13.6.war %TOMCAT_HOME%\webapps\ebms-adapter.war
```

De ebms-adapter EbMS interface is vervolgens bereikbaar op [http://localhost:8080/ebms-adapter/ebms](http://localhost:8080/ebms-adapter/ebms).

De ebms-adapter soap interface is vervolgens bereikbaar op [http://localhost:8080/ebms-adapter/service/cpa](http://localhost:8080/ebms-adapter/service/cpa) en [http://localhost:8080/ebms-adapter/service/ebms](http://localhost:8080/ebms-adapter/service/ebms).

## EbMS Admin Console

De EbMS Admin Console is een losse applicatie waarmee de EbMS adapter kan worden beheerd. Via de Admin Console kunnen de CPA’s worden beheerd, kunnen verschillende EbMS functies worden uitgevoerd (zoals het uitvoeren van een EbMS ping, EbMS berichten versturen en bekijken) en kan het EbMS verkeer worden gemonitord.

![image]({{ site.baseurl }}/assets/images/ebms-admin-rproxy.png)

### Configureren ebms-admin.properties  
Zie [ebms-admin.properties]({{ site.baseurl }}{% link properties/ebms-admin.md %})

### Installeren EbMS Admin Console

#### Linux
```sh
mkdir /opt/ebms-admin
cp ebms-admin-2.13.6.jar ebms-admin.properties /opt/ebms-admin
cp <jdbc-driver>.jar /opt/ebms-admin
echo "nohup java -cp <jdbc-driver>.jar:ebms-admin-2.13.6.jar nl.clockwork.ebms.admin.Start -port 8000 &" > /opt/ebms-admin/start.sh
chmod u+x /opt/ebms-admin/start.sh
```

#### Windows
```powershell
mkdir c:\ebms-admin
copy ebms-admin.properties c:\ebms-admin\
copy ebms-admin-2.13.6.jar c:\ebms-admin\
copy <jdbc-driver>.jar c:\ebms-admin\
echo java -cp <jdbc-driver>.jar;ebms-admin-2.13.6.jar nl.clockwork.ebms.admin.Start -port 8000 > c:\ebms-admin\start.bat
```

### Starten EbMS Admin Console

#### Linux
```sh
cd /opt/ebms-admin
./start.sh
```

#### Windows
```powershell
cd c:\ebms-admin
start.bat
```

De admin console is vervolgens bereikbaar op [http://localhost:8000/](http://localhost:8000/).
