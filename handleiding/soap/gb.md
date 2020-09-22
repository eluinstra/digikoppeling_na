---
sort: 3
---

# Grote Berichten SOAP Interface

###### sendFile(filename,contentType,url,maxSize,compression)
{: #sendFile}
Verwerkt file `filename` uit directory `gb.fileShare` tot een transaction in directory `gb.workingDir`, slaat deze transaction op in de database voor verzending en geeft een transactionId terug.
Vervolgens wordt de transactie synchroon verzonden door de verzend service.
Het aanmaken van een transaction betekent dat het bestand wordt gezipped in volumes van maximaal maxSize bytes groot  
`contentType` bevat het contentType van de file filename  
`url` bevat de url waar de transaction naar toe wordt geupload  
`compression` bevat de compressie methode die wordt gebruikt (`NONE|ZIP4J`)

Voorbeeld bericht
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns="http://www.nationaalarchief.nl/digikoppeling/gb/2.3">
   <soapenv:Header/>
   <soapenv:Body>
             <ns1:sendFile>
         <filename>5MB.bin</filename>
         <contentType>application/binary</contentType>
         <url>https://gb-acpt.nationaalarchief.nl/gb/tenant_na/upload/</url>
         <maxSize>1048576</maxSize>
         <compression>NONE</compression>
      </ns1:sendFile>
   </soapenv:Body>
</soapenv:Envelope>
```

###### getStatus(transactionId)
{: #getStatus}
Geeft de status terug van de transaction `transactionId`
- `PENDING` - wacht voor verdere verwerking
- `PACKAGING` - bezig met packagen bestand
- `READY_TO_SEND` - klaar voor verzending
- `SUCCEEDED` - de transaction is (dus alle zipvolumes waaruit de transaction bestaat zijn) succesvol verzonden
- `FAILED` - het verzenden van de transaction (dus van 1 van de bestanden waaruit de transaction bestaat) is gefaald

###### getTransactionIds(status)
{: #getTransactionIds}
Geeft de transactionsIds van de transactions met status `status` of van alle statussen als status is leeg

###### resumeTransaction(transactionId)
{: #resumeTransaction}
Resume `FAILED` transaction `transactionId`. Gaat verder bij de `FAILED` zipvolume

###### getDataReferenceRequest(transactionId)
{: #getDataReferenceRequest}
Geeft Grote Berichten Standaard DataReferenceRequest van transaction `transactionId` terug. Dit bericht bevat een beschrijving van het bestand en de zipvolumes waaruit deze bestaat (zie Voorstel Grote Berichten Standaard).

###### resendTransaction(transactionId,dataReferenceResponse)
{: #resendTransaction}
Resend de zipvolumes van transaction `transactionId` die zijn niet goed zijn ontvangen (`status=ERROR`), zoals beschreven in dataReferenceResponse

###### deleteTransaction(transactionId)
{: #deleteTransaction}
Delete transaction `transactionId` uit het systeem (=de directory `gb.workingDir` en de transaction tabel)
