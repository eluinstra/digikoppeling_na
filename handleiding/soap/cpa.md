---
sort: 1
---

# CPA SOAP Interface

De CPA SOAP Service biedt de volgende functies

###### validateCPA(cpa)
{: #validateCPA}
valideert cpa `cpa`

###### insertCPA(cpa, overwrite)
{: #insertCPA}
slaat cpa `cpa` op in de EbMS adapter. Als overwrite is true en de cpa bestaat, dan wordt deze overschreven. De functie geeft de cpaId van de cpa terug.

###### deleteCPA(cpaId)
{: #deleteCPA}
verwijdert cpa met cpaId `cpaId` uit de EbMS adapter

###### getCPAIds()
{: #getCPAIds}
geeft een lijst van alle cpaIds terug die in de EbMS adapter zijn opgeslagen

###### getCPA(cpaId)
{: #getCPA}
geeft de cpa terug met cpaId `cpaId`

###### setURLMapping(urlMapping)
{: #setURLMapping}
slaat urlMapping `urlMapping` op in de EbMS adapter. De urlMapping mapt de source url op de destination url

###### deleteURLMapping(source)
{: #deleteURLMapping}
verwijdert urlMapping met source url `source` uit de EbMS adapter

###### getURLMappings()
{: #getURLMappings}
geeft een lijst met alle urlMappings terug die in de EbMS adapter zijn opgeslagen
