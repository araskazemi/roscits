<a name="top"></a>

# C-ITS översikt
<mark>Cooperative Intelligent Transport Systems (C-ITS)</mark> avser system där fordon, infrastruktur och andra trafikanter utbyter information i realtid för att förbättra trafiksäkerhet, framkomlighet och effektivitet i transportsystemet. Till skillnad från traditionella ITS-lösningar, som i huvudsak bygger på centraliserad informationsspridning, möjliggör C-ITS ett distribuerat informationsutbyte där flera aktörer både producerar och konsumerar data.

C-ITS är ett samlingsbegrepp för teknologier och standardiserade kommunikationslösningar som stödjer olika former av kommunikation, inklusive mellan fordon (V2V), mellan fordon och infrastruktur (V2I), samt mellan fordon och omgivande system och trafikanter (V2X), exempelvis via backend-system och tjänsteplattformar (V2N). I praktiken innebär detta att information kan delas om exempelvis hårda inbromsningar, halt väglag, tillfälliga hastighetsbegränsningar, olyckor, vägarbeten eller andra trafikstörningar.

Syftet är att skapa ett mer koordinerat och situationsmedvetet transportsystem där aktörer kan agera på aktuell och tillförlitlig information. Genom lågfördröjd kommunikation kan C-ITS bidra till ökad trafiksäkerhet, förbättrad framkomlighet och minskad miljöpåverkan. Tekniken utgör även en viktig möjliggörare för utvecklingen av högre nivåer av fordonsautomation.

``` 🔥 NYTT! ```

## C-ITS i en global kontext
C-ITS bör förstås som en global utvecklingsriktning. Olika regioner använder delvis olika begrepp, tekniska profiler och styrningsmodeller, men de adresserar i grunden samma behov: att skapa säkert, skalbart och interoperabelt informationsutbyte mellan transportsystemets aktörer.

På standardiseringssidan bidrar organisationer som ISO och CEN med övergripande ITS-standardisering och arkitekturramverk, medan ETSI har en särskilt viktig roll i Europa genom standarder för meddelanden, kommunikationsprofiler och säkerhetsmekanismer. 

I USA används ofta begreppet Connected Vehicles eller V2X snarare än C-ITS. Där har utvecklingen länge drivits genom pilotprogram och initiativ från U.S. Department of Transportation, bland annat med fokus på V2V- och V2I-tillämpningar, trafiksäkerhet och säkerhetsarkitekturen SCMS, Security Credential Management System. SCMS bygger, liksom EU:s modell, på PKI-principer för att möjliggöra betrodd kommunikation mellan aktörer och enheter.

Kina har i sin tur i hög grad fokuserat på C-V2X och en mer integrerad modell där fordon, väg och moln kopplas samman i ett gemensamt ekosystem. Utvecklingen beskrivs ofta som “vehicle-road-cloud integration” och är nära kopplad till ambitioner kring intelligenta uppkopplade fordon och avancerad automatisering.

EU:s ekosystem för C-ITS utgör en kombination av policy, standardisering och teknisk infrastruktur som syftar till att möjliggöra säker och interoperabel kommunikation mellan aktörer inom transportsektorn. Det är utformat för att stödja ett brett spektrum av användningsfall, från trafiksäkerhetsrelaterade varningar till mer avancerade tjänster för trafikstyrning och prioritering.

En central utgångspunkt i EU:s arbete med C-ITS är behovet av gränsöverskridande interoperabilitet. Fordon och infrastruktur ska kunna kommunicera och förstå varandra oavsett vilket medlemsland de befinner sig i. Detta ställer krav på harmoniserade regelverk, gemensamma tekniska specifikationer och en samordnad tillitsinfrastruktur.

På policynivå har EU etablerat ramar genom ITS-direktivet (2010/40/EU) och efterföljande delegerade akter. Dessa kompletteras av riktlinjer och samarbetsinitiativ, såsom C-ITS Platform, där medlemsstater, industri och andra intressenter gemensamt utvecklar principer för införande.

Standardisering utgör en bärande del av ekosystemet. Organisationer som ETSI och CEN utvecklar tekniska standarder som specificerar kommunikationsprotokoll, meddelandeformat och säkerhetsmekanismer. En särskilt viktig komponent är [EU-CCMS](euccms.md) som utformar en gemensam Public Key Infrastructure (PKI). Denna säkerställer att meddelanden kan verifieras av mottagaren samtidigt som avsändarens integritet skyddas.

``` 🔥 NYTT! ```

## Olika angreppssätt för C-ITS
Implementationer av C-ITS runtom i världen skiljer sig åt i fråga om policy, teknikval, spektrumreglering, säkerhetsarkitektur och graden av central styrning. Europa har i hög grad fokuserat på interoperabilitet över nationsgränser, gemensamma standarder och en europeisk tillitsinfrastruktur. Detta har lett till ett ekosystem där ETSI-standarder, C-Roads-profiler och EU-CCMS tillsammans utgör viktiga byggstenar för införande och samverkan.

I USA har utvecklingen historiskt varit starkt kopplad till Connected Vehicle-program, pilotinföranden och säkerhetsapplikationer. Även där är tillit en central fråga, men arkitekturen har organiserats kring SCMS snarare än EU-CCMS. Fokus har ofta legat på praktiska pilotmiljöer, såsom stadstrafik, motorvägskorridorer och särskilda säkerhetsanvändningsfall.

Kina skiljer sig genom en mer uttalad inriktning mot C-V2X, cellulär kommunikation och kopplingen mellan fordon, vägkantssystem och molnplattformar. Detta ger en delvis annan tyngdpunkt än den europeiska modellen, där både kortdistanskommunikation och IP-baserad kommunikation kan förekomma inom ramen för ett interoperabelt ekosystem.

Trots dessa skillnader finns betydande likheter. Samtliga regionala implementationer behöver hantera samma grundläggande frågor:
- vilka aktörer som ska få delta,
- hur deras behörighet ska verifieras,
- hur meddelanden ska skyddas mot manipulation,
- hur systemet ska kunna skalas över organisatoriska och geografiska gränser.

Gemensamt för dessa angrepssätt är behovet av att balansera säkerhet, integritet och spårbarhet. Fordon och infrastruktursystem måste kunna lita på mottagen information, samtidigt som systemen inte bör möjliggöra onödig övervakning eller spårning av enskilda fordon eller trafikanter.

En viktig slutsats är därför att regionala skillnader främst ligger i styrning, teknikval och implementation, medan de underliggande problemen är gemensamma. C-ITS är i praktiken ett globalt interoperabilitets- och tillitsproblem, där varje region utvecklar sin egen lösning utifrån lokala regelverk, marknadsförutsättningar och teknisk strategi.

## Informationsutbyte baserat på ETSI-meddelanden
Inom C-ITS utbyts säkerhets- och trafikrelaterad information genom standardiserade meddelanden som definieras inom ETSI och används i operativa C-ITS-tjänster. Kommunikation kan ske både via direktkommunikation (meddelanden sänds ofta som broadcast inom räckvidd) och via mobilnät (distributionen sker vanligtvis via backend-system med unicast eller multicast). Det finns alltså två huvudvägar, vilka också kan kombineras:
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
2. <mark>Transportlager</mark> (Federation, t ex mTLS): Säkerställer att kommunikation endast etableras mellan betrodda organisationer och Interchange-noder.

Kopplingen mellan dessa lager hanteras via Registration Authorities (RA), som binder samman tekniska identiteter (certifikat) med organisatorisk tillit och åtkomst till interoperabla noder.

För att samtidigt uppnå säkerhet och skydd av personuppgifter använder C-ITS i Europa ett gemensamt PKI [EU-CCMS](eussms.md) med kortlivade pseudonyma certifikat. Detta innebär att meddelanden kan verifieras utan att avslöja fordonets eller förarens identitet.

:arrow_right: [Nästa](cits_in_eu.md)

<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  
