---
sort: 4
---

# Technische beschrijving Grote Berichten koppeling

Dit hoofdstuk bevat een technische beschrijving van de Grote Berichten koppeling met het Nationaal Archief.

Met de Grote Berichten koppeling kunnen bestanden worden uitgewisseld tussen het e-Depot van het Nationaal Archief en de (keten) partners van het Nationaal Archief. Het Nationaal Archief biedt hiervoor een Grote Berichten Server waarnaar klanten bestanden kunnen uploaden voor het e-Depot via de Grote Berichten adapter en waarvan Klanten bestanden kunnen downloaden van het e-Depot dmv HTTP GET.

De EbMS koppeling moet voldoen aan *Koppelvlakstandaard Grote Berichten voor Digikoppeling 3.0* en *Voorstel wijziging Grote Berichten standaard 0.4*. De koppeling gebruikt HTTPS. Hiervoor zijn beveiligings keys en certificaten nodig in de vorm van PKI Overheidcertificaten.

![image](/assets/images/gb-adapter.png)

## Open Source Grote Berichten adapter en console
Voor de realisatie van de Grote Berichten koppeling met het Nationaal Archief kan gebruik worden gemaakt van de nog source Grote Berichten adapter (zie [Installeren Grote Berichten adapter]({{ site.baseurl }}{% link handleiding/installatie-gb-adapter.md %})) en de Grote Berichten console (zie [Installeren Grote Berichten console]({{ site.baseurl }}{% link handleiding/installatie-gb-console.md %})). Hierna volgt een kort technische beschrijving van de open source Grote Berichten adapter en console.

De open source Grote Berichten adapter heeft een SOAP interface voor het verzenden van bestanden via de Grote Berichten adapter vanuit één of meerdere applicaties, zoals de Grote Berichten console.

![image](/assets/images/gb.png)

De Grote Berichten adapter slaat de metadata van een Grote Berichten transactie op in een database. De volgende databases worden ondersteund
- HSQLDB (test only)
- MSSQL (zie [Grote Berichten MSSQL Scripts]({{ site.baseurl }}{% link handleiding/database/gb-mssql.md %}))
- MySQL (zie [Grote Berichten MySQL Scripts]({{ site.baseurl }}{% link handleiding/database/gb-mysql.md %}))
- Oracle (zie [Grote Berichten Oracle Scripts]({{ site.baseurl }}{% link handleiding/database/gb-oracle.md %}))
- Postgresql (zie [Grote Berichten Postgres Scripts]({{ site.baseurl }}{% link handleiding/database/gb-postgres.md %}))

De bestanden zelf worden op disk opgeslagen.

De SOAP interface de Grote Berichten service voor het verzenden en beheren van Grote Berichten transacties (zie [Grote Berichten SOAP Interface]({{ site.baseurl }}{% link handleiding/soap/gb.md %}))

De Grote Berichten console pakt bestanden op uit de File Share, stuurt de Grote Berichten console aan om deze te versturen naar het NA en stuurt de EbMS adapter aan om via de uploadExportBestand EbMS operatie de metadata (DataReferenceRequest) te versturen naar het NA. Ook verwerkt het de uploadExportBestandBevestiging EbMS operatie afkomstig van het NA voor het succesvol bevestigen van de upload van het bestand of het eventueel herversturen van het bestand via de Grote Berichten adapter.

De Grote Berichten console slaat de metadata over de bestanden op in de database. De volgende databases worden ondersteund
- HSQLDB (test only)
- MSSQL (zie [Grote Berichten MSSQL Scripts]({{ site.baseurl }}{% link handleiding/database/gb-console-mssql.md %}))
- MySQL (zie [Grote Berichten MySQL Scripts]({{ site.baseurl }}{% link handleiding/database/gb-console-mysql.md %}))
- Oracle (zie [Grote Berichten Oracle Scripts]({{ site.baseurl }}{% link handleiding/database/gb-console-oracle.md %}))
- Postgresql (zie [Grote Berichten Postgres Scripts]({{ site.baseurl }}{% link handleiding/database/gb-console-postgres.md %}))

## Grote Berichten Service Omgevingen

Het Nationaal Archief heeft een aantal Grote Berichten Service omgevingen waarmee (keten)partners kunnen koppelen. Er zijn een productie en een TED omgeving op het internet ontsloten en er zijn een productie en een TED omgeving op de Haagse Ring aangesloten. Hierna volgt een overzicht van deze omgevingen. Vraag de actuele gegevens op bij het Nationaal Archief.

### Grote Berichten Koppeling PRD Internet

|URL [IP Adres]|	|
|Certificaat|
|Certificate Chain|

### Grote Berichten Koppeling TED Internet

|URL [IP Adres]|	|
|Certificaat|
|Certificate Chain|

### Grote Berichten Koppeling PRD Haagse Ring

|URL [IP Adres]|	|
|Certificaat|
|Certificate Chain|

### Grote Berichten Koppeling TED Haagse Ring

|URL [IP Adres]|	|
|Certificaat|
|Certificate Chain|
