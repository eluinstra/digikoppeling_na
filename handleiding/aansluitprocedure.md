---
sort: 2
---

# Aansluitprocedure EbMS

Dit hoofdstuk beschrijft de aansluit procedure voor de EbMS koppeling met het Nationaal Archief. 

Om aan te kunnen sluiten op de EbMS koppeling Archiefregistratie moet er een CPA worden geregistreerd die het contract bevat tussen 2 EbMS endpoints. Het genereren van de CPA wordt gedaan door het Nationaal Archief. Voor het genereren van een CPA is o.a. de volgende informatie nodig
- Organisatie-identificatienummer (OIN)
- Tenant_ID of ISIL-code
- URL en Server IP Adres EbMS endpoint Productie en TED/Acceptatie omgeving
- Client IP Adres(sen) EbMS adapter Prodcutie en TED/Acceptatie omgeving
- PKI overheidscertificaten Productie en TED/Acceptatie omgeving

Om aan te kunnen sluiten op de Grote Berichten Service is de volgende informatie nodig
- Client IP Adres Grote Berichten Adapter Productie en TED/Acceptatie omgeving

Vul hiervoor het aansluitformulier [Digikoppeling Aansluitformulier]({{ site.baseurl }}{% link handleiding/aansluitformulier.md %}) in en stuur deze op naar het Nationaal Archief.

Er wordt per omgeving één CPA per organisatie gegenereerd. Dit betekent dat voor een organisatie die uit meerdere suborganisaties bestaat dus maar één CPA wordt gegenereerd. Er kunnen dus meerdere (keten)partner Identificatie Nummers per organisatie worden opgegeven in het aansluitformulier.

## Aanmaken PKI Overheidcertificaten

De (voorbeeld)instructies hieronder gaan uit van het gebruik van openssl.  Eerst worden lokaal een private key en een Certificate Signing Request (CSR) aangemaakt. Vervolgens wordt het CSR getekend door een certificate authority. Het resultaat daarvan is een certificaat. De lijst van certificate authorities die PKI Overheidcertificaten uitgeven is [hier](https://www.logius.nl/diensten/pkioverheid/aanschaffen/) te vinden. Zie voor windows ook [Handleiding aanmaak CSR](https://adoc.pub/handleiding-aanmaak-csr1d8b75ccc31a6b6a7527d73e72a78a1e9150.html) van digidentity.

### Aanmaken private key + CSR

Maak eerst een custom openssl.conf bestand aan. Zie [openssl.conf]({{ site.baseurl }}{% link handleiding/openssl-conf.md %}) voor een voorbeeld.

Voer het volgende commando uit
```sh
openssl req -newkey rsa:2048 -sha256 -nodes -keyout <organisatie>.key -out <organisatie>.csr -config openssl.cnf
```

### Check key

Voer het volgende commando uit
```sh
openssl rsa -in <organisatie>.key -check
```

### Check CSR

Voer het volgende commando uit
```sh
openssl req -text -noout -verify -in <organisatie>.csr
```
