<a name="top"></a>

# Inledning
Transportsystemet genomgår en snabb digitalisering där fordon, infrastruktur och trafikledningssystem i allt högre grad förväntas samverka i realtid. Teknologier som artificiell intelligens, uppkopplade fordon, autonoma transportlösningar och smart infrastruktur förändrar hur människor och varor förflyttas. 

Cooperative Intelligent Transport Systems (C-ITS) är en central del i denna utveckling och möjliggör informationsutbyte mellan aktörer för att förbättra trafiksäkerhet, framkomlighet och effektivitet.

Denna utveckling skapar stora möjligheter, men medför också flera komplexa utmaningar. C-ITS bygger på att många olika aktörer – fordonstillverkare, väghållare, kommuner, statliga myndigheter och specialiserade fordon – kan utbyta information på ett tillförlitligt och interoperabelt sätt. Dessa aktörer verkar ofta inom olika organisatoriska, juridiska och tekniska domäner, med skilda uppdrag, förutsättningar och krav.

En grundläggande utmaning är därför att etablera tillit för informationsutbyte mellan aktörer som inte har en direkt relation till varandra. För att ett fordon ska kunna agera på information från ett trafiksystem, eller för att ett trafikljus ska prioritera ett utryckningsfordon, krävs att mottagaren kan verifiera både avsändarens identitet och att informationen är oförändrad och giltig i sitt sammanhang. Detta ställer höga krav på gemensamma tillitsramverk, identitetshantering och tekniska infrastrukturer, såsom PKI-baserade certifikatsystem.

Utöver tillitsfrågan finns även betydande utmaningar kopplade till interoperabilitet. C-ITS är i grunden ett globalt koncept, men implementeras inom regionala och nationella ramar. EU har etablerat ett eget ramverk, inklusive [EU-CCMS](#euccms), för att möjliggöra en gemensam tillitsinfrastruktur. Samtidigt behöver nationella implementationer förhålla sig till både europeiska krav och lokala behov, vilket skapar spänningar mellan standardisering och flexibilitet.

Ett ytterligare problemområde rör införande och adoption. Många av de tänkta nyttorna med C-ITS förutsätter en hög grad av införande och samordning mellan aktörer. I praktiken präglas sektorn av befintliga system, etablerade kommunikationsmönster och organisatoriska gränser som gör det svårt att införa nya tekniska lösningar fullt ut. Höga krav på tillitsgranskning, certifiering och specialiserad utrustning i fordon och infrastruktur kan utgöra trösklar, särskilt för mindre aktörer.

Mot denna bakgrund syftar kapitlet till att beskriva den etablerade målbilden för C-ITS samt EU-CCMS roll i att möjliggöra en gemensam europeisk tillitsinfrastruktur. I rapportens Del B – Analys av roller och implementation – analyseras hur olika implementeringsstrategier kan stödja en gradvis och realistisk utveckling. Analysen belyser relationen mellan EU:s tillitsinfrastruktur och nationella initiativ samt undersöker alternativa angreppssätt som kan sänka trösklarna för deltagande samtidigt som grundläggande krav på säkerhet och interoperabilitet upprätthålls.


## Cooperative Intelligent Transport Systems (C-ITS)
<mark>Cooperative Intelligent Transport Systems (C-ITS)</mark> avser system där fordon, infrastruktur och andra trafikanter utbyter information i realtid för att förbättra trafiksäkerhet, framkomlighet och effektivitet i transportsystemet. Till skillnad från traditionella ITS-lösningar, som i huvudsak bygger på centraliserad informationsspridning, möjliggör C-ITS ett distribuerat informationsutbyte där flera aktörer både producerar och konsumerar data.

C-ITS är ett samlingsbegrepp för teknologier och standardiserade kommunikationslösningar som stödjer olika former av kommunikation, inklusive mellan fordon (V2V), mellan fordon och infrastruktur (V2I), samt mellan fordon och omgivande system och trafikanter (V2X), exempelvis via backend-system och tjänsteplattformar (V2N). I praktiken innebär detta att information kan delas om exempelvis hårda inbromsningar, halt väglag, tillfälliga hastighetsbegränsningar, olyckor, vägarbeten eller andra trafikstörningar.

Syftet är att skapa ett mer koordinerat och situationsmedvetet transportsystem där aktörer kan agera på aktuell och tillförlitlig information. Genom lågfördröjd kommunikation kan C-ITS bidra till ökad trafiksäkerhet, förbättrad framkomlighet och minskad miljöpåverkan. Tekniken utgör även en viktig möjliggörare för utvecklingen av högre nivåer av fordonsautomation.

``` 🔥 NYTT! ```

### C-ITS i en global kontext
C-ITS bör förstås som en global utvecklingsriktning. Olika regioner använder delvis olika begrepp, tekniska profiler och styrningsmodeller, men de adresserar i grunden samma behov: att skapa säkert, skalbart och interoperabelt informationsutbyte mellan transportsystemets aktörer.

På standardiseringssidan bidrar organisationer som ISO och CEN med övergripande ITS-standardisering och arkitekturramverk, medan ETSI har en särskilt viktig roll i Europa genom standarder för meddelanden, kommunikationsprofiler och säkerhetsmekanismer. 

I USA används ofta begreppet Connected Vehicles eller V2X snarare än C-ITS. Där har utvecklingen länge drivits genom pilotprogram och initiativ från U.S. Department of Transportation, bland annat med fokus på V2V- och V2I-tillämpningar, trafiksäkerhet och säkerhetsarkitekturen SCMS, Security Credential Management System. SCMS bygger, liksom EU:s modell, på PKI-principer för att möjliggöra betrodd kommunikation mellan aktörer och enheter.

Kina har i sin tur i hög grad fokuserat på C-V2X och en mer integrerad modell där fordon, väg och moln kopplas samman i ett gemensamt ekosystem. Utvecklingen beskrivs ofta som “vehicle-road-cloud integration” och är nära kopplad till ambitioner kring intelligenta uppkopplade fordon och avancerad automatisering.

EU:s ekosystem för C-ITS utgör en kombination av policy, standardisering och teknisk infrastruktur som syftar till att möjliggöra säker och interoperabel kommunikation mellan aktörer inom transportsektorn. Det är utformat för att stödja ett brett spektrum av användningsfall, från trafiksäkerhetsrelaterade varningar till mer avancerade tjänster för trafikstyrning och prioritering.

En central utgångspunkt i EU:s arbete med C-ITS är behovet av gränsöverskridande interoperabilitet. Fordon och infrastruktur ska kunna kommunicera och förstå varandra oavsett vilket medlemsland de befinner sig i. Detta ställer krav på harmoniserade regelverk, gemensamma tekniska specifikationer och en samordnad tillitsinfrastruktur.

På policynivå har EU etablerat ramar genom ITS-direktivet (2010/40/EU) och efterföljande delegerade akter. Dessa kompletteras av riktlinjer och samarbetsinitiativ, såsom C-ITS Platform, där medlemsstater, industri och andra intressenter gemensamt utvecklar principer för införande.

Standardisering utgör en bärande del av ekosystemet. Organisationer som ETSI och CEN utvecklar tekniska standarder som specificerar kommunikationsprotokoll, meddelandeformat och säkerhetsmekanismer. En särskilt viktig komponent är [EU-CCMS](#euccms) som utformar en gemensam Public Key Infrastructure (PKI). Denna säkerställer att meddelanden kan verifieras av mottagaren samtidigt som avsändarens integritet skyddas.

``` 🔥 NYTT! ```

### Olika angreppssätt för C-ITS
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

<a name="messages"></a>

### Informationsutbyte baserat på ETSI-meddelanden
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

### Säkerhetsarkitektur
Den säkerhetsmodell som används i ett federerat C-ITS-ekosystem består av två kompletterande men separata tillitsmodeller:

:one: Tillit till information (för meddelandesäkerhet)

:two: Federativ tillit till organisationer (för backendintegrationer och vidareförmedling av information)

#### Tillit till information
Inom operativa C-ITS-implementationer enligt europeiska ramverk distribueras meddelanden som kryptografiskt signerade meddelanden i enlighet med ETSI TS 103 097. Detta möjliggör verifiering av avsändarens identitet samt säkerställer meddelandets integritet och autenticitet. För att samtidigt uppnå säkerhet och skydd av personuppgifter använder C-ITS i Europa ett gemensamt PKI [EU-CCMS](#euccms) med kortlivade pseudonyma certifikat. Detta innebär att meddelanden kan verifieras utan att avslöja fordonets eller förarens identitet.

EU-CCMS ansvarar för tillit till information och säkerställer att varje enskilt meddelande är autentiskt, oförändrat och utfärdat av en behörig part, oberoende av hur det transporteras. Detta inkluderar alla stationer och signerade meddelanden samt tillhörande hantering av identitet, certifikat, behörigheter och meddelandeverifiering enligt ETSI-standarder och den europeiska tillitsmodellen.

#### Federativ tillit till organisationer
Federation används för att etablera organisatorisk tillit och säker kommunikation mellan backend-system, Interchange-noder och organisatoriska domäner över IP-baserade nätverk. Detta etableras typiskt genom mTLS och federerad identitet mellan de ingående organisationerna. Federationen är på så sätt ett separat tillitslager ovanpå EU-CCMS och används inte för verifiering av signerade ETSI-meddelandena i sig. Den används för att skydda och autentisera de IP-baserade kommunikationskanalerna mellan backend-system.

#### Bindning mellan meddelandesäkerhet och organisatorisk tillit
Kopplingen mellan dessa modeller hanteras via Registration Authorities (RA), som binder samman tekniska identiteter (certifikat) med organisatorisk tillit och åtkomst till interoperabla noder. RA säkerställer
- registrering av metadata om identitets- och livscykelhantering av stationer och deras behörigheter inom C-ITS-domänen, och
- registrering av metadata och certifikat om backend-system och Interchange-noder, vilka hanteras utanför EU-CCMS med separata federativa tillitsmekanismer och federationstjänster.

I denna struktur är stationen den logiska entiteten som signerar och verifierar meddelanden inom EU-CCMS. En station kan vara:
- en fysisk enhet, exempelvis ett fordon eller en vägkantsutrustning, eller
- en centraliserad ITS-station implementerad i ett backend-system.

Interchange-noder och andra federativa backend-komponenter är på så sätt inte stationer i den gemensamma PKI-strukturen (EU-CCMS), utan utgör ett transportlager mellan organisatoriska domäner, vilka utbyter information med varandra i en federation.

<a name="cits_in_eu"></a>

## Det europeiska ramverket för C-ITS
EU:s ekosystem för C-ITS utgör en kombination av policy, standardisering och teknisk infrastruktur som syftar till att möjliggöra säker och interoperabel kommunikation mellan aktörer inom transportsektorn. Det är utformat för att stödja ett brett spektrum av användningsfall, från trafiksäkerhetsrelaterade varningar till mer avancerade tjänster för trafikstyrning och prioritering.

En central utgångspunkt i EU:s arbete med C-ITS är behovet av gränsöverskridande interoperabilitet. Fordon och infrastruktur ska kunna kommunicera och förstå varandra oavsett vilket medlemsland de befinner sig i. Detta ställer krav på harmoniserade regelverk, gemensamma tekniska specifikationer och en samordnad tillitsinfrastruktur.

På policynivå har EU etablerat ramar genom ITS-direktivet (2010/40/EU) och efterföljande delegerade akter. Dessa kompletteras av riktlinjer och samarbetsinitiativ, såsom C-ITS Platform, där medlemsstater, industri och andra intressenter gemensamt utvecklar principer för införande.

Standardisering utgör en bärande del av ekosystemet. Organisationer som ETSI och CEN utvecklar tekniska standarder som specificerar kommunikationsprotokoll, meddelandeformat och säkerhetsmekanismer. En särskilt viktig komponent är [EU-CCMS](#euccms) som utformar en gemensam Public Key Infrastructure (PKI). Denna säkerställer att meddelanden kan verifieras av mottagaren samtidigt som avsändarens integritet skyddas.

### ITS-direktivet 
EU:s ITS-direktiv (2010/40/EU) och efterföljande delegerade akter utgör den övergripande regulatoriska ramen för införandet av intelligenta transportsystem inom unionen. Direktivet syftar till att säkerställa interoperabilitet, standardisering och effektivt införande av ITS-tjänster över nationsgränser. 

I den senaste uppdateringen har särskilt fokus lagts på samverkande, uppkopplade och automatiserade transportsystem, där C-ITS utgör en central komponent. Direktivet ställer krav på medlemsstater att möjliggöra tillgång till relevanta data, säkerställa interoperabla tjänster och stödja utvecklingen av säker kommunikation mellan aktörer i transportsystemet. 

För C-ITS innebär detta att nationella implementationer behöver anpassas till gemensamma europeiska specifikationer, både avseende meddelandeformat, kommunikation och säkerhet. Direktivet driver därmed behovet av harmoniserade lösningar och samordning mellan medlemsstater. 

### Meddelandesäkerhet
[EU-CCMS](#euccms) är ett gemensamt europeiskt PKI-baserat säkerhetssystem som hanterar digitala certifikat för samverkande intelligenta transportsystem (C-ITS) inom EU. Det säkerställer gränsöverskridande interoperabilitet genom att möjliggöra verifiering av att meddelanden är autentiska, oförändrade och utfärdade av en behörig part, samtidigt som avsändarens integritet skyddas.

EU-CCMS är en förutsättning för interoperabilitet mellan länder och aktörer inom C-ITS, men innebär samtidigt betydande krav på både teknisk implementation och organisatorisk struktur. Varje land ansvarar för organisering av registrering, policyer och administration av de aktörer och stationer som ansluts till infrastrukturen.


``` 🔥 UPDATERING! ```
### Nationella C-ITS-domän
Den nationella (eller organisatoriska) C-ITS-domänen utgör den organisatoriska och administrativa struktur inom vilken aktörer, stationer och tillitsrelationer hanteras. Domänen är inte en separat PKI-root i EU-CCMS, utan etableras genom styrning, ansvarsfördelning och processer för registrering och certifikathantering.

En nationell domän omfattar typiskt:
- nationella eller organisatoriska RA-funktioner (Registration Authority),
- avtal och organisatoriska överenskommelser,
- styrning och efterlevnad av krav och policyer,
- tilldelning och administration av roller,
- incidenthantering och operativa processer.

Domänen definieras ytterst av domänägarens kontroll över vilka aktörer som får delta och under vilka förutsättningar. Detta inkluderar ansvar för:
- vilka organisationer som får agera RA,
- vilka aktörer och stationer som får registreras,
- vilka EA- och AA-funktioner som är godkända att utfärda certifikat inom domänen,
- nationella policykrav och säkerhetsregler,
- hantering av incidenter och avvikelser.

Den nationella domänen fungerar därmed som ett lager mellan den europeiska tillitsinfrastrukturen och de operativa aktörer som använder C-ITS-tjänster. Även om tilliten till meddelandenas autenticitet och integritet ytterst baseras på certifikat och tillitskedjor inom EU-CCMS och ECTL krävs nationell eller organisatorisk styrning för att säkerställa att registrering, ansvar och operativa processer fungerar i praktiken.

Utformningen av en nationell domän kan skilja sig mellan medlemsstater beroende på organisatoriska förutsättningar, ansvarsfördelning och befintlig systemarkitektur. Vissa länder har valt mer centraliserade modeller medan andra verkar i en mer distribuerad struktur där flera aktörer behöver samverka inom samma domän.

### Interchange-noder
Interchange är inte en PKI-aktör, utan fungerar snarare som en broker eller federationstjänst för transport av IP-baserade meddelanden.

Interchange-noder ansvarar för att vidareföremedla ETSI-meddelanden. Validering av signaturer enligt ETSI TS 103 097 är valfri och kan tillämpas vid behov. Signering och verifiering av meddelandens autenticitet och integritet är krav som behöver hanteras av den avsändande respektive mottagande stationen. I praktiken förutsätter många use case att meddelanden är signerade i enlighet med gällande säkerhetsramverk (t ex EU-CCMS Security Policy).

Interchange kan beskrivas som en eller flera noder som ingår i en federation. Tillit etableras utanför EU-CCMS PKI genom en kombination av avtalsbaserade överenskommelser, tekniska säkerhetsmekanismer och konfiguration.

En Interchange-nod:
- tar emot ett C-ITS-meddelande via IP,
- vid behov verifierar signaturen (ETSI TS 103 097),
- kontrollerar relevans (till exempel position, meddelandetyp),
- distribuerar vidare meddelandet till en annan nod via IP. 

Interchange-noder kan även användas för att utbyta meddelanden mellan noder i olika C-ITS-domäner, till exempel inom samarbeten som NordicWay. Detta möjliggör interoperabilitet mellan nationella eller regionala implementationer utan att dessa behöver dela samma tekniska eller organisatoriska kontrollstruktur, men ställer samtidigt krav på tydliga överenskommelser kring tillit, ansvar och informationsutbyte.

### Svensk implementering av C-ITS
Sverige har under flera år deltagit i europeiska C-ITS-initiativ, bland annat genom NordicWay-projekten och C-Roads, där fokus har legat på test och validering av tjänster och tekniska lösningar. 

Den svenska kontexten kännetecknas av en relativt decentraliserad struktur, där ansvar för olika delar av transportsystemet är fördelat mellan flera aktörer, inklusive statliga myndigheter, kommuner, industri och tjänsteleverantörer. Detta skiljer sig från vissa andra länder där ansvar och implementation är mer centraliserade. 

Den tekniska mognaden är generellt hög, och flera användarfall är redo för införande. Samtidigt kvarstår utmaningar kopplade till hur ett nationellt C-ITS-system ska organiseras, särskilt avseende ansvarsfördelning, tillitsstruktur och långsiktig drift. 

Tidigare projekt har identifierat dessa utmaningar på en övergripande nivå. I denna rapport konkretiseras de ytterligare genom analys och praktisk implementering, med fokus på vad som krävs för att gå från pilotverksamhet till operativ drift i Sverige. 

``` ⚠️ KOM IHÅG! ```

<mark>Skriv ett stycke med länkar till de olika förslagen för implementering i rapportens del B</mark> 

### Utmaningar

#### Införandegrad: nyttan växer när många fordon och vägar är uppkopplade.
C-ITS bygger på nyttan av att “alla pratar samma språk” – men värdet blir stort först när många bilar och vägar är med.

Hönan-och-ägget-problemet: Fordonstillverkare tvekar att lägga in tekniken om infrastrukturen är begränsad, och väghållare tvekar att investera i utrustning om få fordon kan använda det.

Exempel: Om endast 8 % av fordon och RSU:er kan varna för halka, då ser 92 % aldrig varningen → liten samhällsnytta. Men vid 30–40 % penetration börjar effekten bli märkbar. Först då blir C-ITS riktigt användbart.

#### Interoperabilitet & tillit
När fordon rör sig mellan städer och länder måste budskapen i meddelandena tolkas på samma sätt. ETSI och CEN har format och regler, men små skillnader i implementation kan skapa problem. Uppkomst av olika dialekter kan medföra at alla inte förstår alltid allt.

Meddelanden måste vara signerade så att mottagaren kan lita på att de är äkta. Det innebär att certifikat som är utfärdat i ett land måste accepteras också av alla andra länder. Om tilliten brister eller om länder börjar införa egna alternativa trust modeller kan man få “tillitsluckor” – till exempel en tysk bil som inte litar på en svensk väginfrastruktur.

#### Styrning och konflikter
Teknikval, certifikathantering och integritetspolicy måste hålla över tid. Det finns dock flera risker:
* EU rekommenderar “hybrid”, dvs att man kombinerar kortdistans (ITS-G5) och mobilnät (LTE/5G). Då täcker man både direkta säkerhetskritiska varningar (annat fordon bromsar framför dig) och tjänster som kräver nät (till exempel trafikinformation från en tjänst i molnet). Industrin har delade åsikter: Vissa förespråkar C-V2X (5G), andra ser värde i ITS-G5. Risken: parallella ekosystem som inte kan prata fullt ut med varandra.
* Det pågår diskussioner om vilket radiospektrum C-ITS ska få, särskilt eftersom mobilindustrin vill ha samma frekvenser för 5G. Det kan skapa regulatoriska konflikter.
* Vägar, fordon, mobilnät och myndigheter ägs av olika aktörer med olika incitament. Det krävs stark samordning.
* Fordon har en livslängd på ca 15–20 år. Infrastruktur ännu längre. Beslut som fattas nu måste hålla i decennier, annars riskerar man “tekniska återvändsgränder”.
* Ekonomisk utmaning: vem betalar? Fordonstillverkare, staten, operatörer, eller en mix? – olika i varje land!

Flera EU-länder har initialt försökt att följa rekommendationerna för implementering av EU-CCMS inom ramen för C-Roads, men har kommit till slutsatsen att komplexiteten och kostnaderna överstiger den kortsiktiga nyttan. Dessa länder har istället valt att realisera C-ITS/ETSI-baserade applikationer genom avtalsbaserade modeller och Interchange-noder. Detta möjliggör å ena sidan tidig nyttorealisering och återanvändning av befintliga system (till exempel trafikljus). Å andra sidan riskerar sådana lösningar att leda till inlåsning och parallella ekosystem, vilket försvårar en fullständig implementering av EU-CCMS. 

En sådan utveckling kan påverka interoperabilitet, fordonsindustrin och möjligheten att etablera en sammanhängande europeisk test- och innovationsmiljö. Om en liknande inriktning skulle tillämpas i Sverige kan det påverka Sveriges förmåga att fungera som testbädd negativt, eftersom en fullt utbyggd EU-CCMS-infrastruktur då skulle saknas på svenska vägar.

<a name="euccms"></a>

## European Union Common Certificate Management System (EU-CCMS)
European Union Common Certificate Management System (EU-CCMS) är EU:s gemensamma säkerhetsinfrastruktur för C-ITS och möjliggör säker och interoperabel kommunikation mellan aktörer och länder genom hantering av digitala certifikat. Det säkerställer att meddelanden är autentiska och skyddar samtidigt användarnas integritet genom pseudonyma certifikat och ett [gemensamt europeiskt ramverk](#cits_in_eu).

Tillit i EU-CCMS baseras på validering av certifikatkedjor mot en uppsättning trust anchors. Dessa trust anchors utgörs av Root CA-certifikat som distribueras via <mark>European C-ITS Trust List (ECTL)</mark>.

En station (till exempel ett fordon eller en vägkantsutrustning) validerar mottagna certifikat genom att kontrollera att:
1. certifikatet är utfärdat av en giltig Certificate Authority (CA),
2. certifikatkedjan kan byggas upp till ett betrott Root CA-certifikat,
3. detta Root CA-certifikat finns i stationens trust store och motsvarar ett Root CA som publiceras i ECTL.

Tillitskedjan inkluderar flera roller:
* <mark>CPA (Certificate Policy Authority)</mark>: ansvarar för policydokument och godkänner Root CAs.
* <mark>TLM (Trust List Manager)</mark>: skapar och publicerar den europeiska certifikatlistan (ECTL) som innehåller alla de Root CAs som är godkända att delta i C-ITS-ekosystemet.
* <mark>CPOC (C-ITS Point of Contact)</mark>: fungerar som nav mellan Root CAs och TLM, tar emot certifikat, publicerar ECTL och tillhandahåller ankre i tillitskedjan (trust anchors).
* <mark>Root CA</mark>: kan vara statliga eller privata aktörer. Utfärdar certifikat till:
    * <mark>EA (Enrolment Authority)</mark>: utfärdar <mark>Enrolment Credentials (EC)</mark> till C-ITS-enheter (fordon och RSU:er).
    * <mark>AA (Authorization Authority)</mark>: utfärdar <mark>Authorisation Tickets (AT)</mark>, som är kortlivade pseudonyma certifikat för att skydda integriteten.

C-ITS-enheter använder EC för identifiering gentemot tillitsinfrastrukturen och AT för att signera och verifiera C-ITS-meddelanden.

### Vad som utmärker EU-CCMS
#### Pseudonymitet och integritetsskydd
Till skillnad från klassisk PKI, där identiteten ofta är knuten till certifikatet, använder C-ITS pseudonyma certifikat (ATs) som byts ofta för att förhindra spårning av fordon. Kopplingen till fordonets verkliga identitet hålls skyddad av EA/AA och exponeras inte i kommunikationen.

#### Korta livstider i nyckelhanteringen
Authorisation Tickets (AT) har kort giltighetstid och måste bytas ofta (sekretesskrav). Detta skiljer sig från traditionella PKI-certifikat som ofta är giltiga i månader eller år.

#### Multirot-struktur och central trust list
Flera Root CAs kan samexistera, men alla listas i en central European Certificate Trust List (ECTL) signerad av TLM. 

#### Separering av roller (EA och AA)
En viktig säkerhetsdesign är separationen mellan enrolment (EC) och authorization (AT) för att undvika att någon enskild aktör kan både identifiera och spåra ett fordon. I en traditionell PKI finns inte denna uppdelning – CA utfärdar certifikat direkt till slutanvändare.

#### Specifika C-ITS-protokoll och standarder
Certifikat och signaturer följer ETSI TS 103 097 och relaterade standarder, optimerade för bandbredd och realtidskrav i fordonskommunikation.
Även särskilda "butterfly key"-mekanismer används för att möjliggöra massgenerering av pseudonyma certifikat.

#### Striktare operativa och fysiska kontroller
Rollerna (Root CAs, EA, AA, TLM) omfattas av detaljerade krav på revision, fysiska säkerhetskontroller och procedurer som fastställs av EU (via CP, Security Policy och CPOC Protocol). Traditionell PKI följer ofta en CA/Browser Forum eller eIDAS-baserad policy, men C-ITS har sin egen europeiska styrmodell.

#### Manuella och fysiska processer för nyckelhantering
Root CA-certifikat lämnas ofta fysiskt (med kurir) till CPOC för att minska risken för kompromettering. Detta är ovanligt i klassisk PKI, där processerna i större utsträckning är automatiserade.


### Övergripande tillitsstruktur
Den övergripande strukturen för tillitsmodellen kan delas i följande tre skikt:

:one: EU-nivå

:two: Nationell domän

:three: Molntjänstförmedlare (som kallas Interchange)

```
────────────────────────────────────────────────────────────
                EUROPEAN LEVEL
────────────────────────────────────────────────────────────

            European Commission
   (Policy, Governance, Legal Framework)
                     │
                     ▼
             Trust List Manager
                     │
                     ▼
                    ECTL
              (EU Trust List)
                     │
                     ▼
           ┌─────────────────────┐
           │  RCA EU             │
           │  (Default Root CA)  │
           └─────────────────────┘
                      │
           ┌──────────┴──────────┐
           ▼                     ▼
   ┌───────────────┐      ┌───────────────┐
   │      EA       │      │      AA       │
   │ Enrollment CA │      │ Authorization │
   │               │      │      CA       │
   └───────────────┘      └───────────────┘
           │                     │
           │                     │
────────────────────────────────────────────────────────────
         NATIONAL C-ITS DOMAIN (e.g. Sweden)
────────────────────────────────────────────────────────────

       Domain Governance and Policy
                     │
                     ▼
        ┌───────────────────────────┐
        │ RA-system (Registration)  │
        │ Identity vetting          │
        │ Station approval          │
        └───────────────────────────┘
                     │
                     ▼
            Certificate Requests
                     │
         ┌───────────┴────────────┐
         ▼                        ▼
        EC                        AT
(Long-term identity)    (Short-term pseudonym)
                     │
                     ▼
              C-ITS STATIONS
    ┌────────────────────────────────┐
    │  Roadside ITS-S                │
    │  Vehicle ITS-S                 │
    │  Traffic signal ITS-S          │
    │  Emergency vehicle ITS-S       │
    └────────────────────────────────┘
                     │
                     ▼
            Signed C-ITS Messages
         (CAM, DENM, MAPEM, SPATEM, etc.)

────────────────────────────────────────────────────────────
           OPTIONAL IP / CLOUD LAYER
────────────────────────────────────────────────────────────

    ┌────────────────────────────────┐
    │                                │
    │   Interchange / Cloud broker   │
    │                                │
    └────────────────────────────────┘
(Not part of trust anchor, but must validate signatures)

```

### Hur PKI-kedjan hänger ihop
PKI-kedjan i EU-CCMS bygger på en multiple root CA-arkitektur med en gemensam trust list.
Det innebär att:
- en svensk station accepterar en fransk station,
- en norsk station accepterar en tysk station,
- och så vidare.

Detta är grunden för interoperabilitet enligt Security Policy.

Förenklat ser tillitskedjan ut så här:

```
 ECTL
   ↓
  RCA
   ↓
EA / AA
   ↓
C-ITS Station Certificates
   ↓
Signed Messages

```

Den gemensamma tilliten kommer dock inte från en gemensam root, utan från en multiple root CA architecture med en gemensam europeisk trusted list, ECTL.

Tillitskedjena kan se ut så här:

```
                     CPA
                      │
                      ▼
              Trust List Manager
                      │
                      ▼
            ECTL (EU Trust List)
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
   Root CA EU    Root CA A      Root CA B
  (EU default)  (e.g. nation)  (e.g. OEM)
        │             │              │
        ▼             ▼              ▼
      EA/AA         EA/AA          EA/AA
        │             │              │
        ▼             ▼              ▼
    Stations      Stations       Stations

```


<a name="cits_roles"></a>

## Roller och rättigheter i C-ITS
För att förstå hur roller och rättigheter hanteras i C-ITS behöver man skilja på tre separata nivåer:

:one: Tekniska roller i PKI (t ex EU-CCMS)

:two: Meddelandetyper och funktionella roller (t ex prioritering av trafikljus)

:three: Applikationsroller (t ex utryckningsfordon)

### Tekniska roller i PKI för meddelandesignering
Tekniska roller för signering av ETSI-meddelanden är infrastrukturella och inte trafikroller.

*Security Policy Release 3.0*, i [det europeiska ramverket för C-ITS](#cits_in_eu), beskriver rollerna i säkerhets- och certifikatsystemet för [EU-CCMS](#euccms), som bland annat reglerar signering av meddelanden.

Internationellt kan det finnas andra PKI-system med motsvarande eller avvikande roller.

### Meddelandetyper och funktionella roller
I C-ITS finns särskilda [meddelandetyper](#messages) och flaggor för olika use cases (som i C-ITS kallas *applikationer*), till exempel:
- Emergency and Service Vehicle Notifications – Emergency or Prioritised Vehicle Approaching (ESVN-EPVA)
- Emergency and Service Vehicle Notifications – Slow Moving Maintenance Vehicle (ESVN-SMMV)
- Emergency Vehicle Priority (SI-EVP)
- Traffic Light Prioritisation (SI-TLP)

> [!IMPORTANT]
> Exempelvis innebär ESVN-EPVA att systemet kan signalera att ett fordon är ett utryckningsfordon. Men det är inte en fri roll som man själv deklarerar, snarare **en egenskap som är kopplad till auktoriserade certifikat**.

### Applikationsroller
En applikation i C-ITS-världen (use case) definieras av:
- Ett syfte (t ex: “Emergency Vehicle Approaching”)
- En meddelandetyp (t ex: DENM)
- Specifika fältvärden (t ex: causeCode = emergencyVehicleApproaching)
- Säkerhetsrättigheter (ITS-AID + SSP)

I certifikatet (AT) finns ett fält som heter `ITS-AID` (ITS Application Identifier). Det anger:
- vilka applikationer stationen får använda, och
- vilka [meddelandetyper](#messages) den får sända.

Det är alltså inte meddelandet i sig, utan rätten att signera (=använda applikationen) som är säkerhetsstyrd.

SSP (Service Specific Permissions) som också ligger i certifikatet (AT) är den mekanism som gör att två stationer kan ha rätt att sända samma meddelandetyp
men med olika behörighetsnivåer.

> [!IMPORTANT]
> ITS-AID	anger vilken applikation som är tillåten. <br />
> SSP	anger vilka roller/underfunktioner inom applikationen som är tillåtna. Mottagande station ansvarar för att tolka SSP och avgöra om ett mottaget meddelande är legitimt i sin kontext.

Strukturen förenklat:
```
Authorization Ticket
 ├─ ITS-AID (vilken applikation)
 ├─ SSP (Service Specific Permissions)
 ├─ Validity
 └─ Signature
```

En C-ITS-station (t ex ett blåljusfordon) får ett Enrollment Certificate (EC) samt ett eller flera Authorization Tickets (AT). En station kan även ha flera AT samtidigt, exempelvis för olika applikationer (ITS-AID).

Certifikatet AT innehåller:
- Applikationsrättigheter
- Tillåtna meddelandetyper
- Eventuella specialattribut
 
Exempelvis ett blåljusfordon får AT som innehåller:
- ITS-AID för CAM
- ITS-AID för DENM
- SSP för `emergencyVehicleRole` inom DENM
- ITS-AID för SREM
- SSP för `emergencyVehicleRole` inom SREM

Det innebär att fordonet får sända: 
- CAM
- DENM med `Code = emergencyVehicleApproaching` (ESVN-EPVA use case)
- SREM och begära prioritet i signalanläggning 

Medan ett vanligt fordon får AT som innehåller:
- ITS-AID för CAM
- ITS-AID för DENM
- SSP som endast tillåter generering av generiska händelser inom DENM (dvs. saknar emergency-relaterade rättigheter)

Det innebär att fordonet får sända:
- CAM
- vissa DENM (t ex `stationary vehicle`, `slippery road`)

Certifikat (AT) i ett vanligt fordon saknar SSP för `emergencyVehicleRole` samt saknar ITS-AID för SREM (och kan därmed inte sända SREM alls).

> [!NOTE]
> Validering av rättigheter sker helt lokalt hos mottagande station baserat på innehåll i certifikatet (AT).

### Styrning av roller och rättigheter
Styrning av roller och rättigheter hanteras i tre lager:

:white_check_mark: **ETSI TS 103 097** definierar hur rättigheter kodas i certifikaten.

:white_check_mark: **Certificate Policy** definierar hur rättigheter får utfärdas.

:white_check_mark: **C-ITS domänpolicy** avgör vem som faktiskt får dessa roller och rättigheter.

Om alla fordon kunde sända “jag är ett utryckningsfordon”, då skulle hela systemet kollapsa säkerhetsmässigt. Därför är rollen kryptografiskt skyddad och måste vara auktoriserad av rätt RA/EA/AA – den måste ligga inom korrekt tillitskedja.

EU definierar: meddelandetyper, certifikatstruktur, tillitsmodell och kryptografi samt interoperabilitetskrav.

Medlemsstaten styr den operativa maktstrukturen inom sin C-ITS-domän. Detta innebär att medlemsstaten:
- Fastställer nationell C-ITS-policy
- Utser och styr RA/EA/AA-struktur
- Avgör vilka aktörer som är legitima (t ex blåljus, kollektivtrafik, vägarbeten)
- Beslutar om roll- och SSP-tilldelning
- Ansvarar för riskbedömning och säkerhetsstyrning
- Hanterar incidenter och revokering
- Integrerar C-ITS med nationell lagstiftning och trafikstyrning
- Fastställer operativa prioriteringsregler
- Avgör acceptans av utländska rättigheter inom nationell infrastruktur

För interoperabilitet mellan medlemsstater krävs harmonisering av ITS-AID och SSP, så att rättigheter kan tolkas korrekt även över nationsgränser. Denna harmonisering sker genom gemensamma profiler och specifikationer som tas fram och valideras inom ramen för C-Roads.


## RA-funktioner för C-ITS-domän
<mark>Registration Authority (RA)</mark> i [EU-CCMS](#euccms) är den funktion som ansvarar för registrering av C-ITS-stationer i systemet.

RA:s uppgifter omfattar normalt:
- verifiering av identitet hos den organisation som driver stationen
- verifiering av behörighet för den aktuella rollen
- registrering av attribut
- vidarebefordran av certifikatbegäran till relevant Certificate Authority

RA utfärdar inte certifikat och ingår inte i certifikatkedjan.  
Certifikat utfärdas av betrodda CAs inom EU-CCMS-infrastrukturen.

RA säkerställer att CA får korrekta uppgifter för att rätt aktör, rätt utrustning och rätt roll och rättigheter kopplas till rätt certifikat enligt Certificate Policy.

Den aktör som kontrollerar RA har i praktiken kontroll över:
- vilka stationer som finns i domänen,
- vilka organisationer som får delta,
- vem som kan identifieras vid incident.

Därför väljer många länder att ha RA nationellt, även om EA och AA kan vara externa.

### Information som en RA hanterar
Utifrån Security Policy och den organisatoriska strukturen i C-Roads kan man dela upp informationen som RA hanterar i följande kategorier:

:one: Identitetsinformation om organisationen

:two: Roll- och rättigheter

:three: Information om C-ITS-stationen

:four: Certifikathanteringsdata

:five: Avtals- och efterlevnadsinformation

:six: Loggar och revisionsspår

#### Identitetsinformation om organisationen
RA måste hantera uppgifter om de organisationer som ingår i C-ITS-domänen, bl a:
- Organisations-ID (teknisk identitet)
- Organisationsnummer (juridisk identitet)
- Organisationsnamn
- Land/jurisdiktion
- Kontaktperson(er)
- Kontaktuppgifter
- Eventuella fullmakter/behörighetsintyg och avtal

Syftet med dessa uppgifter är att säkerställa:
- att endast legitima organisationer registreras,
- att organisationen har rätt att agera i en viss roll (t ex road operator, emergency authority etc.),
- att den omfattas av rätt nationell rättsordning,
- att villkor och ansvarsfördelning och sanktioner är reglerade.

Detta är klassisk PKI-registreringsinformation, men i C-ITS är kopplingen till roll och funktion särskilt viktig.

#### Roll- och rättigheter
Stationer i C-ITS har olika [roller och rättigheter](#cits_roles). RA behöver ha en förteckning över:
- Typer av C-ITS-stationer som kan registreras i domänen (RSU, OBU, central station, etc.)
- Roller som kan förekomma i trust-modellen (road operator, OEM, service provider, etc.)
- Eventuella särskilda behörigheter (t ex blåljusprioritet, trafiksignalstyrning, m.m.)

Detta är kritiskt eftersom:
- olika roller kan få olika certifikattyper
- vissa roller kan ha särskilda rättigheter (t ex SREM/SSEM för blåljus)
- felaktig registrering kan skapa allvarliga säkerhetsrisker

#### Information om C-ITS-stationen
RA behöver skapa förutsättningar för att certifikat kan knytas till en konkret teknisk entitet.

Exempel på data som registreras:
- Unikt stations-ID (som kan skapas av RA eller av organisationen som äger stationen)
- Serienummer
- Tillverkare
- Modell
- Firmware-/hårdvaruversion
- Säkerhetscertifiering (Common Criteria / ISO 15408 enligt Security Policy 

Detta möjliggör:
- spårbarhet
- spärrning vid kompromettering
- livscykelhantering

> [!IMPORTANT]
> RA registrerar inte certifikaten – känner inte till stationen EC och AT.
>- RA registrerar information om stationen och tilldelar/registrerar en stationidentifierare.
>- EA använder den identifieraren när EC utfärdas och kopplar den till certifikatet.
>- Det är alltså EA/AA som har loggar som kopplar certifikat till stationen.
>- EA kan tekniskt utfärda EC utan att känna till stationens verkliga identitet — bara ett RA-godkänt identifieringsvärde.

#### Certifikathanteringsdata
RA hanterar metadata kring certifikatutgivning, t ex:
- Certifikatförfrågan (CSR)
- Koppling till rätt CA
- Certifikattyp (Enrollment Certificate, Authorization Ticket, etc.)
- Giltighetstid
- Återkallandeinformation
- Loggning av beslut

Detta är kärnan i registreringsprocessen och RA som funktion – att säkerställa korrekt koppling mellan identitet och certifikat och livscykelhantering.

> [!NOTE]
> RA ser och verifierar den publika nyckeln i samband med CSR/registrering för Enrollment Certificate (EC), men RA behöver inte nödvändigtvis lagra nyckeln permanent som en egen datapost.

#### Avtals- och efterlevnadsinformation
Eftersom C-ITS bygger på en gemensam trust-modell behövs även:
- Intyg om efterlevnad av Security Policy 
- Åtagande att följa Certificate Policy
- Eventuella nationella tillägg baserat på domänägarens godkännande
- Incidentrapporteringsansvar

Detta är särskilt viktigt när domänen styrs genom avtal, det vill säga när varje organisation frivilligt väljer att ansluta sig till och ingå i domänen, snarare än att omfattas av bindande regelverk eller lagstiftning.

#### Loggar och revisionsspår
En RA måste enligt god säkerhetspraxis hantera:
- Vem som godkänt registrering
- När beslut fattades
- Underlag för beslut
- Ändringshistorik
- Revokeringar

Detta är avgörande för juridisk hållbarhet, spårbarhet och incidenthantering.

### Livscykelhantering av stationsinformation i ett RA-verksamhetssystem
En C-ITS-station genomgår typiskt följande livscykelfaser i RA-verksamhetssystemet:

:one: Förberedande registrering (organisation + roll)

:two: Initial registrering av station

:three: Certifikatgodkännande

:four: Operativ drift

:five: Uppdatering/ändringshantering

:six: Spärrning/avstängning

:seven: Avregistrering/avveckling

:eight: Arkivering och gallring

#### Förberedande registrering (organisation + roll)
Innan en station kan registreras måste organisationen vara godkänd i RA.

Processen kan vara enligt följande steg:
1. Organisation ansöker om att bli registrerad.
2. RA verifierar, juridisk identitet, behörig företrädare, roll i C-ITS-ekosystemet.
3. RA tilldelar organisations-ID.
4. Organisationens behöriga administratör registreras.

Resultat: Organisationen får rätt att registrera stationer inom sitt mandat.

#### Initial registrering av station
När organisationen är godkänd kan station registreras.

Processen kan vara enligt följande steg:
1. Organisation initierar registrering via RA-gränssnitt och lämna information om:
    - Stations-ID (eller begäran om generering)
    - Serienummer
    - Tillverkare och modell
    - Firmwareversion
    - Typ av station (RSU/OBU/central)
    - Säkerhetscertifieringsuppgifter
    - Geografisk placering (för RSU)
2. CSR (Certificate Signing Request) laddas upp.
3. RA kontrollerar att:
    - stationstypen är tillåten för organisationens roll,
    - hårdvaran är godkänd enligt policy,
    - inga dubbletter förekommer.
4. RA loggar hela processen.

Resultat: Stationen registreras och tilldelas status Preliminär.

#### Certifikatgodkännande
RA godkänner certifikatutfärdande.

Processen kan vara enligt följande steg:
1. RA verifierar CSR.
2. RA säkerställer korrekt koppling (Organisation → Roll → Station → Certifikattyp)
3. RA godkänner begäran.
4. CA utfärdar Enrollment Certificate.
5. Stationens status uppdateras.

Resultat: Stationen tilldelas status Aktiv.

#### Operativ drift
Under drift hanterar systemet:
- Certifikatförnyelser (EA/AA)
- Utfärdande av Authorization Tickets (AA)
- Loggning av certifikataktivitet (EA/AA)
- Incidentrapportering (RA + övriga funktioner)

RA ansvarar för att:
- hålla register över stationer uppdaterat
- övervaka avvikelser
- initiera spärrning av certifikat

#### Uppdatering/ändringshantering
Information om en station kan behöva uppdateras, t ex firmwareuppdatering, hårdvarubyte, ändrad geografisk placering, byte av ägare/organisation, ändrad roll eller funktion.

Processen kan vara enligt följande steg:
1. Organisation initierar ändringsärende.
2. RA bedömer om:
    - endast metadata uppdateras
    - nytt certifikat krävs
    - ny säkerhetsvalidering krävs
3. Ändringen loggas och versioneras.

> [!NOTE]
> Vid större förändring måste gamla certifikat spärras och nyregistrering eller ny CSR kan krävas.

#### Spärrning/avstängning
En spärrning kan initieras av organisationen själv, RA, incidenthantering eller nationell säkerhetsfunktion.
Det kan handla om komprometterad nyckel, manipulerad station, otillåten användning, felaktig registrering, m.m.

Processen kan vara enligt följande steg:
1. RA beslutar om spärrning.
2. Certifikat återkallas (CRL/OCSP).
3. Stationens status ändras till Spärrad.
4. Incident dokumenteras.

#### Avregistrering/avveckling
När en station tas ur drift kan processen kan vara enligt följande steg:
1. Organisation anmäler avveckling.
2. RA verifierar status att station inte är aktiv samt att certifikat är spärrade
3. RA ändrar status till Avvecklad.

Resultat: Operativa kopplingar stängs.

Hur länge historisk information ska bevaras beslutas av domänägaren och är kopplat till revisionskrav.

#### Arkivering och gallring
RA måste:
- arkivera registreringsdata
- bevara revisionsspår
- följa CITS-domänens arkiv- och gallringsregler
- följa relevant lagstiftning, såsom GDPR, NIS2 och nationella säkerhetsskyddskrav

Gallring kan ske enligt fastställd bevarandetid, som fastställs utifrån gällande lagstiftning och säkerhetsklassning.

### Teknisk gränssnitt mellan RA och CA
Certifikatutfärdare behöver inte ha direktåtkomst till RA-verksamhetssystemet eller RA-databasen.

Ett korrekt designat EU-CCMS bygger på:
- rollseparation,
- minimal informationsdelning, och
- kryptografisk validering.

EA/AA måste ha mekanismer för att hantera nyregistreringar samt få kännedom om spärrade EC, ändrad behörighet och policyändringar. 

Anslutning mellan certifikatutfärdare och RA regleras genom avtal och måste uppfylla gällande krav enligt domänens policy. Kommunikationen måste säkras för att förhindra att CSR manipuleras under överföringen och behöver därför följa samma nivå som i Certificate Policy.

Det finns tre situationer som kräver kommunikation mellan RA och CA.

:one: **Nyregistrering**

När en station registreras första gången: <br />
RA → godkänner <br />
EA → utfärdar EC <br />

Här sker ett kontrollerat informationsutbyte.

:two: **Statusförändring**

Om något ändras hos RA, t ex station avregistreras, roll ändras, organisation mister behörighet eller vid säkerhetsincident: <br />
RA → uppdatera status <br />
EA/AA → sluta utfärda certifikat <br />

Det kan exempelvis ske via:
- periodisk synkronisering,
- push-notifikationer/prenumerationer,
- status-API.

Det är alltså en statuskoppling, inte en fullständig databasdelning som krävs.

:three: **Incident**
Vid missbruk kan Misbehaviour Authority (MA) involveras. RA kan behöva verifiera den ursprungliga registreringen, medan AA kan behöva upphöra med att utfärda nya AT. Detta förutsätter samverkan mellan aktörerna, men inte nödvändigtvis teknisk integration i realtid i samtliga delar.

### Hur CSR används i RA-processen
### Enrollment CSR
1. Stationen genererar nyckelpar i HSM, Secure Element eller TPM-liknande miljö.
2. Stationen skapar CSR:
    - Inkluderar publik nyckel
    - Inkluderar begärda attribut
    - Signerar med privat nyckel
3. CSR skickas till RA. Det kan vara (beroende på implementation):
    - station → RA → EA, eller
    - station → EA med RA som “godkännandesteg”/policy-gate 
4. RA validerar CSR genom att kontrollera:
    - att stationen är registrerad
    - att rollen är korrekt
    - att certifikattyp är tillåten
    - att CSR är korrekt signerad
    - att nyckelparametrar uppfyller policy
5. RA godkänner sedan begäran till CA.
6. EA utfärdar Enrollment Certificate (EC).
7. RA uppdaterar sina poster i RA-verksamhetssystemet.

#### Authorization CSR
1. Stationen använder sitt EC för att autentisera sig mot AA-tjänsten.
2. Stationen genererar en batch av pseudonym-nycklar.
3. Stationen skapar en signerad Authorization Ticket Request (CSR-liknande fil för begäran om en eller flera certifikat).
4. AA genomför kryptografisk kontroll och policykontroll.
5. RA har en indirekt roll genom att ha definierat stationens roll och rättigheter, men styrs i regel via EC. Domänen har dock möjlighet att ställa krav på AA att denne måste göra uppslag i RA-policy och/eller RA-attributtjänst.
6. AA utfärdar pseudonymer och stationen får tillbaka en batch AT som kan användas för att signera meddelanden (CAM, DENM, etc.)

> [!IMPORTANT]
> En angripare kan försöka byta ut publik nyckel, ändra attribut eller begära fel certifikattyp. RA kan inte lita på attribut i CSR okritiskt och måste kontrollera attribut i CSR mot sitt eget register och på så sätt säkerställa att rätt rollattribut finns i certifikatet.

### Spårning vid incidenter
När en station skickar meddelanden (t .ex. CAM eller DENM) används AT-certifikat (pseudonymer) som inte avslöjar stationens verkliga identitet. Om något allvarligt inträffar, såsom falska varningar eller attacker, behöver det vara möjligt att spåra avsändaren utan att bryta pseudonymiteten under normal drift. Detta kan RA, EA och AA göra tillsammans genom en stegvis spårning av identiteter. Stegen kan beskrivas enligt nedan:
1. Man börjar med certifikatet i meddelandet som ger information om utfärdaren samt certifikatets serienummer.
2. Med serienumret vet AA vilken EC som användes för att begära pseudonymcertifikatet.
3. EA vet vilken station som har tilldelats EC.
4. RA vet vilken organisation som registrerade stationen.



<p>&nbsp;</p>


----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)
