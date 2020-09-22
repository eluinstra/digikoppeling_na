---
sort: 2
---

# EbMS SOAP Interface

De EbMS SOAP Service biedt de volgende functies

###### ping(cpaId, fromParty, toParty)
{: #ping}
voert een EbMS ping actie uit voor cpa `cpaId` van party `fromParty` naar party `toParty`

###### sendMessage(messageContent)
{: #sendMessage}
verzendt het bericht `messageContent` als EbMS bericht. Deze functie geeft het messageId van het EbMS bericht terug.

###### getMessageIds(messageContext, maxNr)
{: #getMessageIds}
geeft een lijst van messageIds terug van berichten met de status `RECEIVED` die voldoen aan het filter `messageContext`. Als `maxNr` wordt meegegeven, dan worden er maximaal maxNr messageIds teruggegeven.

###### getMessage(messageId, process)
{: #getMessage}
geeft het bericht terug met messageId `messageId` (in de vorm van messageContent). Als `process` is `true`, dan krijgt het bericht de status `PROCESSED`, waardoor deze niet meer in de lijst van getMessageIds terug wordt gegeven.

###### processMessage(messageId)
{: #processMessage}
zet de status van het bericht met messageId `messageId` op `PROCESSED`, waardoor deze niet meer in de lijst van [getMessageIds](#getmessageids) terug wordt gegeven.

###### processMessages(messageIds)
{ :#processMessages}
zie [processMessage](#processmessage), maar dan voor een lijst van `messageIds`

###### getMessageEvents(messageContext, eventTypes, maxNr)
{: #getMessageEvents}
geeft de events terug die voldoen aan het filter `messageContext` en aan de eventTypes `eventTypes`. Als `maxNr` wordt meegegeven, dan worden er maximaal maxNr events teruggegeven. De mogelijke eventTypes zijn
- `RECEIVED` - als een bericht in ontvangen
- `DELIVERED` - als een bericht succesvol is verstuurd
- `FAILED` - als een bericht een fout terugkrijgt tijdens het verzenden
- `EXPIRED` - als een bericht niet kon worden verzonden binnen de in de CPA afgesproken aantal pogingen en tijd.

###### processMessageEvent(messageId)
{: #processMessageEvent}
zet processed is `true` voor event met messageId `messageId`, waardoor deze niet meer in de lijst van [getMessageEvents](#getmessageevents) (en [getMessageIds](#getmessageids)) terug wordt gegeven.

###### processMessageEvents(messageIds)
{: #processMessageEvents}
zie [processMessageEvent](#processmessageevent), maar dan voor een lijst van `messageIds`
