---
sort: 1
---

# Technische beschrijving EbMS koppeling

Dit hoofdstuk bevat een technische beschrijving van de EbMS koppeling met het Nationaal Archief.

Met de EbMS koppeling kunnen berichten secure en reliable worden uitgewisseld tussen het e-Depot van het Nationaal Archief en de (keten)partners van het Nationaal Archief.

De EbMS koppeling moet voldoen aan *Koppelvlakstandaard ebMS voor Digikoppeling 3.0*. De koppeling gebruikt HTTPS en de berichten worden gesigneerd. Hiervoor zijn beveiligings keys en certificaten nodig in de vorm van PKI Overheidcertificaten.

![image](/assets/images/ebms-overview.png)

## Open Source EbMS adapter

Voor de realisatie van de EbMS koppeling met het Nationaal Archief kan gebruik worden gemaakt van de open source EbMS adapter (zie [Installatie EbMS Adapter]({{ site.baseurl }}{% link handleiding/installatie-ebms.md %})). Hierna volgt een kort technische beschrijving van de open source EbMS adapter.

De open source EbMS adapter heeft 2 interfaces
- EbMS interface om te communiceren met een andere EbMS adapter
- SOAP interface voor het verzenden en ontvangen van berichten via de EbMS adapter vanuit   één of meerdere keten (partner) applicaties.

![image](/assets/images/ebms-rproxy1.png)

De EbMS adapter slaat de binnengekomen en uitgaande berichten op in een database. De volgende databases worden ondersteunt
- HSQLDB (test only)
- MSSQL (zie [EbMS MSSQL Scripts]({{ site.baseurl }}{% link handleiding/database/ebms-mssql.md %}))
- MySQL (zie [EbMS MySQL Scripts]({{ site.baseurl }}{% link handleiding/database/ebms-mysql.md %})))
- Oracle (zie [EbMS Oracle Scripts]({{ site.baseurl }}{% link handleiding/database/ebms-oracle.md %})))
- Postgresql (zie [EbMS Postgres Scripts]({{ site.baseurl }}{% link handleiding/database/ebms-postgres.md %})))

De SOAP interface bevat 2 services
- CPA service voor het beheren van CPA’s en endpoint url’s (zie [CPA SOAP Interface]({{ site.baseurl }}{% link handleiding/soap/cpa.md %}))
- EbMS service voor het verzenden, ontvangen en gereedmelden van berichten (zie [EbMS SOAP Interface]({{ site.baseurl }}{% link handleiding/soap/ebms.md %}))

De proxy server is nodig om de EbMS interface te ontsluiten via het internet en de SOAP interface te blokkeren vanaf het internet. 

## EbMS Omgevingen

Het Nationaal Archief heeft een aantal EbMS omgevingen waarmee (keten)partners kunnen koppelen. Er zijn een productie en een TED omgeving op het internet ontsloten en er zijn een productie en een TED omgeving op de Haagse Ring aangesloten. Hierna volgt een overzicht van deze omgevingen.

![image](/assets/images/ebms-rproxy2.png)

Het Client IP Adres bevat het IP adres waarmee de EbMS adapter van het Nationaal Archief verbinding maakt met de Proxy/EbMS adapter van de (keten)partner.

URL en Server IP Adres bevatten respectievelijk de URL en het IP Adres waarop de Proxy/EbMS adapter van het Nationaal Archief bereikbaar is.

Certificaat is het Server Certificaat van het Nationaal Archief.

Certificate Chain is het Server Certificate Chain van het Nationaal Archief.

Vraag de actuele gegevens op bij het Nationaal Archief.

### EbMS Koppeling PRD Internet

|Client IP Adres(sen)|	|
|URL [Server IP Adres]|
|Certificaat|
|Certificate Chain|

### EbMS Koppeling TED Internet

|Client IP Adres(sen)|	|
|URL [Server IP Adres]|
|Certificaat|
|Certificate Chain|

### EbMS Koppeling PRD Haagse Ring

|Client IP Adres(sen)|	|
|URL [Server IP Adres]|
|Certificaat|
|Certificate Chain|

### EbMS Koppeling TED Haagse Ring

|Client IP Adres(sen)|	|
|URL [Server IP Adres]|
|Certificaat|
|Certificate Chain|

