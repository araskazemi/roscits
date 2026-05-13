<a name="top"></a>

# Det europeiska ramverket för C-ITS
EU:s ekosystem för C-ITS utgör en kombination av policy, standardisering och teknisk infrastruktur som syftar till att möjliggöra säker och interoperabel kommunikation mellan aktörer inom transportsektorn. Det är utformat för att stödja ett brett spektrum av användningsfall, från trafiksäkerhetsrelaterade varningar till mer avancerade tjänster för trafikstyrning och prioritering.

En central utgångspunkt i EU:s arbete med C-ITS är behovet av gränsöverskridande interoperabilitet. Fordon och infrastruktur ska kunna kommunicera och förstå varandra oavsett vilket medlemsland de befinner sig i. Detta ställer krav på harmoniserade regelverk, gemensamma tekniska specifikationer och en samordnad tillitsinfrastruktur.

På policynivå har EU etablerat ramar genom ITS-direktivet (2010/40/EU) och efterföljande delegerade akter. Dessa kompletteras av riktlinjer och samarbetsinitiativ, såsom C-ITS Platform, där medlemsstater, industri och andra intressenter gemensamt utvecklar principer för införande.

Standardisering utgör en bärande del av ekosystemet. Organisationer som ETSI och CEN utvecklar tekniska standarder som specificerar kommunikationsprotokoll, meddelandeformat och säkerhetsmekanismer. En särskilt viktig komponent är [EU-CCMS](euccms.md) som utformar en gemensam Public Key Infrastructure (PKI). Denna säkerställer att meddelanden kan verifieras av mottagaren samtidigt som avsändarens integritet skyddas.

## ITS-direktivet 
EU:s ITS-direktiv (2010/40/EU) och efterföljande delegerade akter utgör den övergripande regulatoriska ramen för införandet av intelligenta transportsystem inom unionen. Direktivet syftar till att säkerställa interoperabilitet, standardisering och effektivt införande av ITS-tjänster över nationsgränser. 

I den senaste uppdateringen har särskilt fokus lagts på samverkande, uppkopplade och automatiserade transportsystem, där C-ITS utgör en central komponent. Direktivet ställer krav på medlemsstater att möjliggöra tillgång till relevanta data, säkerställa interoperabla tjänster och stödja utvecklingen av säker kommunikation mellan aktörer i transportsystemet. 

För C-ITS innebär detta att nationella implementationer behöver anpassas till gemensamma europeiska specifikationer, både avseende meddelandeformat, kommunikation och säkerhet. Direktivet driver därmed behovet av harmoniserade lösningar och samordning mellan medlemsstater. 

## EU-CCMS
European Union Common Certificate Management System (EU-CCMS) är ett gemensamt europeiskt PKI-baserat säkerhetssystem som hanterar digitala certifikat för [samverkande intelligenta transportsystem (C-ITS)](cits.md) inom EU. Det säkerställer gränsöverskridande interoperabilitet genom att möjliggöra verifiering av att meddelanden är autentiska, oförändrade och utfärdade av en behörig part, samtidigt som avsändarens integritet skyddas.

EU CCMS är en förutsättning för interoperabilitet mellan länder och aktörer inom C-ITS, men innebär samtidigt betydande krav på både teknisk implementation och organisatorisk struktur. Varje land ansvarar för organisering av registrering, policyer och administration av de aktörer och stationer som ansluts till infrastrukturen.

### Tillit och säkerhet
Tillit i EU-CCMS baseras på validering av certifikatkedjor mot en uppsättning trust anchors. 
Dessa trust anchors utgörs av Root CA-certifikat som distribueras via <mark>European C-ITS Trust List (ECTL)</mark>.

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

### Vad som utmärker EU-CCMS jämfört med klassisk PKI
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

``` 🔥 UPDATERAT! ```
## Nationella C-ITS-domän
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

## Interchange-noder
Interchange är inte en PKI-aktör, utan fungerar snarare som en broker eller federationstjänst för transport av IP-baserade meddelanden.

Interchange-noder ansvarar för att vidareföremedla ETSI-meddelanden. Validering av signaturer enligt ETSI TS 103 097 är valfri och kan tillämpas vid behov. Signering och verifiering av meddelandens autenticitet och integritet är krav som behöver hanteras av den avsändande respektive mottagande stationen. I praktiken förutsätter många use case att meddelanden är signerade i enlighet med gällande säkerhetsramverk (EU CCMS Security Policy).

Interchange kan beskrivas som en eller flera noder som ingår i en federation. Tillit etableras utanför EU-CCMS PKI genom en kombination av avtalsbaserade överenskommelser, tekniska säkerhetsmekanismer och konfiguration.

En Interchange-nod:
- tar emot ett C-ITS-meddelande via IP,
- vid behov verifierar signaturen (ETSI TS 103 097),
- kontrollerar relevans (till exempel position, meddelandetyp),
- distribuerar vidare meddelandet till en annan nod via IP. 

Interchange-noder kan även användas för att utbyta meddelanden mellan noder i olika C-ITS-domäner, till exempel inom samarbeten som NordicWay. Detta möjliggör interoperabilitet mellan nationella eller regionala implementationer utan att dessa behöver dela samma tekniska eller organisatoriska kontrollstruktur, men ställer samtidigt krav på tydliga överenskommelser kring tillit, ansvar och informationsutbyte.

## Svensk implementering av C-ITS
Sverige har under flera år deltagit i europeiska C-ITS-initiativ, bland annat genom NordicWay-projekten och C-Roads, där fokus har legat på test och validering av tjänster och tekniska lösningar. 

Den svenska kontexten kännetecknas av en relativt decentraliserad struktur, där ansvar för olika delar av transportsystemet är fördelat mellan flera aktörer, inklusive statliga myndigheter, kommuner, industri och tjänsteleverantörer. Detta skiljer sig från vissa andra länder där ansvar och implementation är mer centraliserade. 

Den tekniska mognaden är generellt hög, och flera användarfall är redo för införande. Samtidigt kvarstår utmaningar kopplade till hur ett nationellt C-ITS-system ska organiseras, särskilt avseende ansvarsfördelning, tillitsstruktur och långsiktig drift. 

Tidigare projekt har identifierat dessa utmaningar på en övergripande nivå. I denna rapport konkretiseras de ytterligare genom analys och praktisk implementering, med fokus på vad som krävs för att gå från pilotverksamhet till operativ drift i Sverige. 

``` ⚠️ KOM IHÅG! ```
<mark>Skriv ett stycke med länkar till de olika förslagen för implementering i rapportens del B</mark> 

## Utmaningar
### Införandegrad: nyttan växer när många fordon och vägar är uppkopplade.
C-ITS bygger på nyttan av att “alla pratar samma språk” – men värdet blir stort först när många bilar och vägar är med.

Hönan-och-ägget-problemet: Fordonstillverkare tvekar att lägga in tekniken om infrastrukturen är begränsad, och väghållare tvekar att investera i utrustning om få fordon kan använda det.

Exempel: Om endast 8 % av fordon och RSU:er kan varna för halka, då ser 92 % aldrig varningen → liten samhällsnytta. Men vid 30–40 % penetration börjar effekten bli märkbar. Först då blir C-ITS riktigt användbart.

### Interoperabilitet & tillit
När fordon rör sig mellan städer och länder måste budskapen i meddelandena tolkas på samma sätt. ETSI och CEN har format och regler, men små skillnader i implementation kan skapa problem. Uppkomst av olika dialekter kan medföra at alla inte förstår alltid allt.

Meddelanden måste vara signerade så att mottagaren kan lita på att de är äkta. Det innebär att certifikat som är utfärdat i ett land måste accepteras också av alla andra länder. Om tilliten brister eller om länder börjar införa egna alternativa trust modeller kan man få “tillitsluckor” – till exempel en tysk bil som inte litar på en svensk väginfrastruktur.

### Styrning och konflikter
Teknikval, certifikathantering och integritetspolicy måste hålla över tid. Det finns dock flera risker:
* EU rekommenderar “hybrid”, dvs att man kombinerar kortdistans (ITS-G5) och mobilnät (LTE/5G). Då täcker man både direkta säkerhetskritiska varningar (annat fordon bromsar framför dig) och tjänster som kräver nät (till exempel trafikinformation från en tjänst i molnet). Industrin har delade åsikter: Vissa förespråkar C-V2X (5G), andra ser värde i ITS-G5. Risken: parallella ekosystem som inte kan prata fullt ut med varandra.
* Det pågår diskussioner om vilket radiospektrum C-ITS ska få, särskilt eftersom mobilindustrin vill ha samma frekvenser för 5G. Det kan skapa regulatoriska konflikter.
* Vägar, fordon, mobilnät och myndigheter ägs av olika aktörer med olika incitament. Det krävs stark samordning.
* Fordon har en livslängd på ca 15–20 år. Infrastruktur ännu längre. Beslut som fattas nu måste hålla i decennier, annars riskerar man “tekniska återvändsgränder”.
* Ekonomisk utmaning: vem betalar? Fordonstillverkare, staten, operatörer, eller en mix? – olika i varje land!

Flera EU-länder har initialt försökt att följa rekommendationerna för implementering av EU-CCMS inom ramen för C-Roads, men har kommit till slutsatsen att komplexiteten och kostnaderna överstiger den kortsiktiga nyttan. Dessa länder har istället valt att realisera C-ITS/ETSI-baserade applikationer genom avtalsbaserade modeller och Interchange-noder. Detta möjliggör å ena sidan tidig nyttorealisering och återanvändning av befintliga system (till exempel trafikljus). Å andra sidan riskerar sådana lösningar att leda till inlåsning och parallella ekosystem, vilket försvårar en fullständig implementering av EU-CCMS. 

En sådan utveckling kan påverka interoperabilitet, fordonsindustrin och möjligheten att etablera en sammanhängande europeisk test- och innovationsmiljö. Om en liknande inriktning skulle tillämpas i Sverige kan det påverka Sveriges förmåga att fungera som testbädd negativt, eftersom en fullt utbyggd EU-CCMS-infrastruktur då skulle saknas på svenska vägar.

:arrow_right: [Nästa](roles_in_cits.md)

<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  
