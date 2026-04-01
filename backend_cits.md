<a name="top"></a>

# Backend-baserad C-ITS med Interchange-noder
Detta avsnitt beskriver en möjlig implementeringsmodell för Sverige där C-ITS/ETSI-baserade applikationer realiseras genom befintliga backend-system, kompletterade med Interchange-noder för informationsutbyte mellan domäner inom en avtalsbaserad modell.

Syftet är att möjliggöra ett avvägt första steg där komplexitet och kostnader hålls nere genom att återanvända befintliga system, samtidigt som backend-systemen ges rollen som centrala C-ITS-stationer med ansvar för att skapa, signera och verifiera ETSI-meddelanden.

Modellen möjliggör tidig nyttorealisering och stegvis införande, utan att i ett första steg fullt ut implementera EU-CCMS, samtidigt som förutsättningar skapas för framtida anpassning till europeiska interoperabilitetsramverk.

## Grundläggande utgångspunkter
Modellen bygger på följande antaganden:

- Befintliga backend-system återanvänds i så stor utsträckning som möjligt.
- Fordon, trafiksignaler och andra fältkomponenter fortsätter att kommunicera med sina backend-system via befintliga gränssnitt och systemlandskap.
- C-ITS-funktionalitet implementeras i backend-systemen, som därmed fungerar som centrala C-ITS-stationer och använder C-ITS PKI för att skapa och verifiera signerade meddelanden.
- Interchange-noder används för att förmedla IP-baserade ETSI-meddelanden mellan domäner och aktörer.
- Interchange utgör ett federativt transportlager för utbyte av C-ITS-meddelanden mellan backend-system.
- Informationsutbyte, federation mellan noder samt anslutning av backend-system regleras genom avtalsbaserade överenskommelser.

Modellen innebär att C-ITS-meddelanden kan skapas och verifieras enligt ETSI, utan att i ett första steg fullt ut implementera EU-CCMS.

## Arkitekturprincip
I denna modell fungerar backend-systemen som centrala C-ITS-stationer och använder EU-CCMS PKI. Det innebär att de ansvarar för att skapa, signera, verifiera och konsumera ETSI-meddelanden i enlighet med relevanta säkerhetskrav.

Ett backend-system behöver därför ha två separata identiteter:

1. **C-ITS-identitet** för att skapa och verifiera signerade meddelanden enligt EU-CCMS.
2. **Transportidentitet** för att kunna autentisera sig mot en Interchange-nod och utbyta meddelanden på ett säkert sätt.

Detta innebär att transporttillit och meddelandetillit behöver hanteras som två olika lager.

## Federationens struktur
I en svensk kontext är det varken realistiskt eller ändamålsenligt att samla all C-ITS-trafik i en gemensam nationell Interchange-nod.

Ansvar, drift och informationsägarskap är redan idag distribuerade mellan flera aktörer:

- Trafikverket ansvarar för statliga vägar och tillhörande infrastruktur.
- Kommuner ansvarar för det kommunala vägnätet, särskilt i urbana miljöer.
- Regioner ansvarar för kollektivtrafik och i många fall ambulansverksamhet.
- Polisen är en statlig aktör med egna system och operativa krav.
- Privata aktörer ansvarar ofta, på uppdrag, för drift, underhåll och utbyggnad av väginfrastruktur.

Att samla all trafik i en enda nod innebär flera utmaningar:

- oklar ansvarsfördelning och styrning mellan organisatoriskt oberoende aktörer
- ökad risk för centraliserade beroenden och single points of failure
- sämre skalbarhet och lägre förändringstakt
- svårare integration med befintliga system
- risk för att lokala och regionala behov underordnas en central modell

En federativ struktur med flera Interchange-noder är därför bättre anpassad till svenska förhållanden.

## Interchange-nodernas omfattning och avgränsning
Interchange-noder bör inte definieras per organisation, exempelvis per kommun, utan utifrån funktionella och operativa domäner.

Det innebär att vissa större aktörer eller operativa domäner kan motivera egna noder, medan andra aktörer ansluter till en gemensam nod inom sin domän.

Omfånget bör bestämmas utifrån hur trafiksystem faktiskt hänger ihop, till exempel per storstadsregion och olika operativa domäner, som exempelvis:

- statlig väginfrastruktur och trafikledning
- urbana trafiksystem och trafiksignaler
- kollektivtrafik och signalprioritering
- blåljus och andra prioriterade fordon
- drift och underhåll

En kommun bör därför inte automatiskt motsvara en egen Interchange-nod. I många fall är det mer ändamålsenligt att flera kommuner delar en gemensam nod, medan större städer eller aktörer med avancerade trafiksystem kan motivera en egen nod.

## Hur informationsutbytet sker
Backend-systemen fungerar som centrala C-ITS-stationer och ansvarar för att skapa, signera och verifiera ETSI-meddelanden. 

Interchange-noder används för att förmedla meddelanden mellan backend-system.

Vid exempelvis signalprioritering för utryckningsfordon:

1. Ett backend-system kopplat till utryckningsverksamhet identifierar behov av prioritet.
2. Backend-systemet genererar relevant ETSI-meddelande för den aktuella applikationen.
3. Meddelandet signeras i backend-systemet med certifikat utfärdade inom EU-CCMS PKI.
4. Backend-systemet publicerar meddelandet till sin Interchange-nod.
5. Interchange-noden vidareförmedlar meddelandet till relevant mottagande nod eller direkt till relevant mottagande backend-system inom sin domän, beroende på konfiguration och behörighet.
6. Det mottagande backend-systemet verifierar meddelandet och omsätter det i lokal funktionalitet, exempelvis styrning av trafiksignal.

Informationsutbytet bygger på två separata lager av tillit som hanteras oberoende av varandra:

:one: Tillit till meddelandets autenticitet och integritet

:two: Tillit till vidareförmedlingen av ETSI-meddelanden

Autenticitet och integritet hos själva ETSI-meddelandet hanteras genom att backend-systemen fungerar som C-ITS-stationer i EU-CCMS och därför kan:

- skapa ETSI-meddelanden
- signera meddelanden
- verifiera mottagna meddelanden
- använda relevanta certifikat och rättigheter

Rätten att ansluta till en Interchange-nod och utbyta information över IP hanteras separat från EU-CCMS, exempelvis genom mTLS mellan backend-system och Interchange-nod.

Det är därför viktigt att skilja mellan rätten att *skapa eller verifiera ett C-ITS-meddelande* och rätten att *ansluta till och använda Interchange*.

## Anslutning av backend-system till Interchange
Backend-system som ska använda Interchange behöver vara kända och godkända av den nod de ansluter till.

Varje Interchange-nod behöver därför ha en funktion för:

- identifiering av anslutande aktörer och system
- godkännande av anslutning
- hantering av certifikat för transporttillit
- tilldelning av rättigheter för publicering och konsumtion
- livscykelhantering, inklusive förändringar och borttagning

Denna funktion motsvarar en lokal registrerings- och onboardingprocess eller en lokal federativ åtkomststyrning inom respektive nod.

## Tillit mellan Interchange-noder
Interchange-noder etablerar tillit till varandra genom en federativ modell, där autentisering och auktorisation baseras på gemensam, signerad metadata. Den federativa modellen kan exempelvis realiseras genom tekniska mekanismer som MATF (Metadata for mTLS Federation).

I en sådan federation:

- noder autentiserar varandra genom mTLS
- tilliten baseras på signerad federationsmetadata
- federationen anger vilka noder, nycklar och certifikat som är godkända

Detta gör det möjligt att federera flera domäner utan att alla måste använda exakt samma certifikatutfärdare, samtidigt som tilliten är styrd och kontrollerad.


## Fördelar med modellen
En federativ, backend-baserad C-ITS med Interchange-noder ger flera möjliga fördelar:

- tidig nyttorealisering i praktiska applikationer
- återanvändning av befintliga backend-system och verksamhetsprocesser
- följsamhet till svensk ansvarsfördelning och organisatoriska förhållanden
- möjlighet till stegvis införande av C-ITS-baserade applikationer 
- minskat behov av omedelbar centralisering av teknik och styrning

## Risker och begränsningar
Modellen innebär också risker och begränsningar:

- tillit på transportnivå måste byggas och styras separat
- lösningen kan skapa inlåsning om den inte utformas med framtida interoperabilitet i åtanke
- olika domäner kan utvecklas i olika takt och med olika profiler
- federationen kräver tydliga avtal, governance och teknisk samordning (vilka inte hanteras inom EU-CCMS PKI)

För att minska dessa risker behöver modellen utformas så att den inte blockerar en framtida utveckling mot bredare europeisk interoperabilitet.



<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  
