<a name="top"></a>
# Vad är C-ITS – och varför spelar det roll?
Cooperative Intelligent Transport Systems (**C-ITS**) är ett samlingsbegrepp för teknologier och standardiserade kommunikationslösningar som möjliggör 
<mark>informationsutbyte:
* mellan fordon (**V2V**)</mark>, t ex “jag bromsar hårt nu!”.
* <mark>mellan fordon och infrastruktur (**V2I**)</mark>, t ex  “hjulspinn/ABS-aktivering – varning för halt väglag!” och “tillfällig hastighetsbegränsning”.
* <mark>mellan fordon och allt runtomkring, andra trafikanter, trafikljus, vägskyltar, driftledningar eller centrala system (**V2X**)</mark>. 

Syftet är att skapa ett mer koordinerat och situationsmedvetet transportsystem där aktörer kan dela realtidsinformation om exempelvis olyckor, 
vägarbeten, väderförhållanden eller plötsliga trafikstörningar.

Genom att möjliggöra lågfördröjd och tillförlitlig kommunikation bidrar C-ITS till ökad trafiksäkerhet, förbättrad framkomlighet och minskad 
miljöpåverkan. Tekniken utgör även en central förutsättning för utvecklingen av högre nivåer av fordonsautomation. Samtidigt ställer C-ITS 
höga krav på interoperabilitet, informationssäkerhet, integritetsskydd och gemensamma styrningsmodeller, särskilt i en gränsöverskridande 
europeisk kontext. Därför är robusta och harmoniserade ramverk avgörande för en säker och effektiv implementering.

EU koordinerar implementering av C-ITS via <mark>C-Roads</mark>, som är en europeisk samarbetsplattform för medlemsstater och väghållningsmyndigheter. 
Initiativet fokuserar på interoperabilitet, gemensamma tekniska specifikationer och praktisk utrullning av kooperativa tjänster, för att säkerställa att 
C-ITS-lösningar fungerar sömlöst och likadant över nationsgränser.

## Informationsutbytet
### Vad skickas?
Inom C-ITS utbyts standardiserade säkerhets- och trafikrelaterade meddelanden. Kommunikationen sker i huvudsak genom broadcast (en-till-alla inom räckvidd). 
Informationen omfattar exempelvis position, hastighet, riktning, inbromsningar, vägarbeten, olyckor, väderförhållanden och andra potentiella faror. 
Meddelandena är tidskritiska och syftar till att öka situationsmedvetenheten i realtid, vilket bidrar till förbättrad trafiksäkerhet, effektivare 
trafikflöden och minskad miljöpåverkan.

C-ITS inbegriper olika meddelandetyper. De viktigaste är:
* <mark>CAM (Cooperative Awareness Message)</mark>: “Här är jag!” – korta pulsar som håller andra uppdaterade om enhetens närvaro och status (position, hastighet, körriktning).
* <mark>DENM (Decentralized Environmental Notification)</mark>: händelsebaserade varningar – t ex “hal is”, “stillastående fordon”, “olycka”.
* <mark>IVIM (Infrastructure-to-Vehicle Information Message)</mark>: ger information från infrastruktur, t ex vägmärken eller vägstatus.
* <mark>SPATEM (Signal Phase and Timing Extended Message)</mark>: beskriver signalstatus (trafikljus) och tidsplan.
* <mark>MAPEM (MAP Extended Message)</mark>: tillhandahåller geometri för korsningar och vägnät.
* <mark>SREM (Signal Request Message)</mark>: begär prioritet i trafiksignaler (t ex för utryckningsfordon eller kollektivtrafik).
* <mark>SSEM (Signal Status Message)</mark>: svar på SREM, anger status på begäran.

Dessa meddelanden är standardiserade i ETSI och används i dagliga C-ITS-tjänster. 

### Hur skickas?
Det finns två huvudvägar, vilka också kan kombineras:
* <mark>ITS-G5 (802.11p)</mark>: dedikerad kortdistanskommunikation, ofta 5.9 GHz, direkt fordon-till-fordon.
* <mark>IP-baserad kommunikation (4G/5G)</mark>: via mobilnät och/eller direkt sidelänk.

Alla C-ITS-meddelanden signeras kryptografiskt enligt ETSI TS 103 097 för att säkerställa integritet och autenticitet.

I Europa förespråkas hybridkommunikation (både ITS-G5 och mobilnät) för att täcka fler scenarier. Utöver att meddelanden måste vara äkta och orörda, 
kräver [det europeiska systemet](euccms.md) att C-ITS inte får avslöja vem föraren är. Europa använder därför ett gemensamt C-ITS-PKI med kortlivade 
pseudonyma certifikat. Själva formatet och säkerhetshuvudet definieras i ETSI TS 103 097. 

## Exempel på användningsfall
Några exempel på anvädningsfall:
* Halka runt kröken: En bil aktiverar antispinn → skickar DENM “halt väglag” → bilar bakom sänker farten innan de passerar isfläcken.
* Stillastående fordon på motorvägen: Bilen som stannat sänder varning → ankommande fordon får tidig heads-up i instrumentklustret. 
* Vägarbete: RSU skickar varning + rekommenderad hastighet → mjukare flöde och färre “sista-sekunden-inbromsningar”. 

## Utmaningar
### Införandegrad: nyttan växer när många fordon och vägar är uppkopplade.
C-ITS bygger på nyttan av att “alla pratar samma språk” – men värdet blir stort först när många bilar och vägar är med.

Hönan-och-ägget-problemet: Fordonstillverkare tvekar att lägga in tekniken om infrastrukturen är begränsad, och väghållare tvekar att investera i utrustning om få fordon kan använda det.

Exempel: Om endast 8 % av fordon och RSU:er kan varna för halka, då ser 92 % aldrig varningen → liten samhällsnytta. Men vid 30–40 % penetration börjar effekten bli märkbar. Först då blir C-ITS riktigt användbart.

### Interoperabilitet & tillit
När fordon rör sig mellan städer och länder måste budskapen i meddelandena tolkas på samma sätt. ETSI och CEN har format och regler, men små skillnader i implementation kan skapa problem. Uppkomst av olika dialekter kan medföra at alla inte förstår alltid allt.

Meddelanden måste vara signerade så att mottagaren kan lita på att de är äkta. Det innebär att certifikat som är utfärdat i ett land måste accepteras också av alla andra länder. Om tilliten brister eller om länder börjar införa egna alternativa trust modeller kan man få “tillitsluckor” – t ex en tysk bil som inte litar på en svensk väginfrastruktur.

### Styrning och konflikter
Teknikval, certifikathantering och integritetspolicy måste hålla över tid. Det finns dock flera risker:
* EU rekommenderar “hybrid”, dvs att man kombinerar kortdistans (ITS-G5) och mobilnät (LTE/5G). Då täcker man både direkta säkerhetskritiska varningar (annat fordon bromsar framför dig) och tjänster som kräver nät (t ex trafikinformation från en tjänst i molnet). Industrin har delade åsikter: Vissa förespråkar C-V2X (5G), andra ser värde i ITS-G5. Risken: parallella ekosystem som inte kan prata fullt ut med varandra.
* Det pågår diskussioner om vilket radiospektrum C-ITS ska få, särskilt eftersom mobilindustrin vill ha samma frekvenser för 5G. Det kan skapa regulatoriska konflikter.
* Vägar, fordon, mobilnät och myndigheter ägs av olika aktörer med olika incitament. Det krävs stark samordning.
* Fordon har en livslängd på ca 15–20 år. Infrastruktur ännu längre. Beslut som fattas nu måste hålla i decennier, annars riskerar man “tekniska återvändsgränder”.
* Ekonomisk utmaning: vem betalar? Fordonstillverkare, staten, operatörer, eller en mix? – olika i varje land!

<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  
