<a name="top"></a>

# C-ITS översikt
Cooperative Intelligent Transport Systems (**C-ITS**) avser system där fordon, infrastruktur och andra trafikanter utbyter information i realtid för att förbättra trafiksäkerhet, framkomlighet och effektivitet i transportsystemet. Till skillnad från traditionella ITS-lösningar, som i huvudsak bygger på centraliserad informationsspridning, möjliggör C-ITS ett distribuerat informationsutbyte där flera aktörer både producerar och konsumerar data.

C-ITS är ett samlingsbegrepp för teknologier och standardiserade kommunikationslösningar som stödjer olika former av kommunikation, inklusive mellan fordon (V2V), mellan fordon och infrastruktur (V2I), samt mellan fordon och omgivande system och trafikanter (V2X), exempelvis via backend-system och tjänsteplattformar (V2N). I praktiken innebär detta att information kan delas om exempelvis hårda inbromsningar, halt väglag, tillfälliga hastighetsbegränsningar, olyckor, vägarbeten eller andra trafikstörningar.

Syftet är att skapa ett mer koordinerat och situationsmedvetet transportsystem där aktörer kan agera på aktuell och tillförlitlig information. Genom lågfördröjd kommunikation kan C-ITS bidra till ökad trafiksäkerhet, förbättrad framkomlighet och minskad miljöpåverkan. Tekniken utgör även en viktig möjliggörare för utvecklingen av högre nivåer av fordonsautomation.

## Informationsutbyte baserat på ETSI-meddelanden
Inom C-ITS utbyts säkerhets- och trafikrelaterad information genom standardiserade meddelanden som definieras inom ETSI och används i operativa C-ITS-tjänster. Kommunikation kan ske både via direktkommunikation (meddelanden ofta sänds som broadcast inom räckvidd) och via mobilnät (distribution vanligtvis via backend-system med unicast eller multicast). Det finns alltså två huvudvägar, vilka också kan kombineras:
* <mark>ITS-G5/PC5</mark>: dedikerad direktkommunikation för korta avstånd.
* <mark>LTE/5G</mark>: nätverksbaserad kommunikation via mobilnät.
I Europa förespråkas hybridkommunikation (ITS-G5 och mobilnät) för att täcka fler scenarier.

Den tekniska grunden för C-ITS är i stor utsträckning etablerad, och fokus har i ökande grad förskjutits från teknikutveckling till frågor om implementering, interoperabilitet och långsiktig drift.

Meddelandena innehåller information om exempelvis position, hastighet, körriktning och inbromsningar, men även händelsebaserad information såsom vägarbeten, olyckor, väderförhållanden och andra potentiella faror. Dessa är tidskritiska och syftar till att öka situationsmedvetenheten i realtid, vilket bidrar till förbättrad trafiksäkerhet, effektivare trafikflöden och minskad miljöpåverkan.

C-ITS omfattar flera typer av standardiserade meddelanden, där de mest centrala är:
* <mark>CAM (Cooperative Awareness Message)</mark>: kontinuerliga statusmeddelanden som informerar om en enhets närvaro och dynamiska tillstånd, såsom position, hastighet och körriktning.
* <mark>DENM (Decentralized Environmental Notification)</mark>: händelsebaserade varningsmeddelanden, exempelvis vid halt väglag, stillastående fordon eller olyckor.
* <mark>IVIM (Infrastructure-to-Vehicle Information Message)</mark>: informationsmeddelanden från infrastruktur, exempelvis vägmärken eller vägstatus.
* <mark>SPATEM (Signal Phase and Timing Extended Message)</mark>: beskriver trafiksignalers aktuella status och tidsförlopp.
* <mark>MAPEM (MAP Extended Message)</mark>: tillhandahåller geometrisk information om vägnät och korsningar.
* <mark>SREM (Signal Request Message)</mark>: används för att begära prioritet i trafiksignaler, exempelvis för utryckningsfordon eller kollektivtrafik.
* <mark>SSEM (Signal Status Message)</mark>: svar på SREM som anger status för begäran.

## Säkerhetsarkitektur
Inom operativa C-ITS-implementationer enligt europeiska ramverk distribueras meddelanden som kryptografiskt signerade meddelanden i enlighet med ETSI TS 103 097. Detta möjliggör verifiering av avsändarens identitet samt säkerställer meddelandets integritet och autenticitet.

Säkerhetsarkitekturen är uppbyggd kring två kompletterande tillitslager som tillsammans skyddar både meddelanden och kommunikationskanaler:
1. <mark>Meddelandelager</mark> (PKI, t ex [EU-CCMS](euccms.md)): Säkerställer att varje enskilt meddelande är autentiskt, oförändrat och utfärdat av en behörig part, oberoende av hur det transporteras.
2. <mark>Transportlager</mark> (Federation, t ex mTLS): Säkerställer att kommunikation endast etableras mellan betrodda organisationer och noder.

Kopplingen mellan dessa lager hanteras via Registration Authorities (RA), som binder samman tekniska identiteter (certifikat) med organisatorisk tillit och åtkomst till interoperabla noder.

För att samtidigt uppnå säkerhet och skydd av personuppgifter använder C-ITS i Europa ett gemensamt PKI [EU-CCMS](eussms.md) med kortlivade pseudonyma certifikat. Detta innebär att meddelanden kan verifieras utan att avslöja fordonets eller förarens identitet.

:arrow_right: [Nästa](cits_in_eu.md)

<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  
