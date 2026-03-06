<a name="top"></a>

# Ett möjligt svenskt alternativ
Inför en svensk implementation av interoperabel C-ITS enligt EU-CCMS uppstår ett antal strategiska frågor kring:
- Domänägarskap
- Registration Authority (RA)
- Enrollment Authority (EA)
- Authorization Authority (AA)
- Nationell rådighet
- Kommunal och regional autonomi
- Offentlig vs privat drift
- Federation vs centralisering

Denna sida syftar till att strukturera frågorna, presentera alternativa organisationsmodeller samt föreslå en rekommenderad strategisk väg för Sverige.

## Grundläggande struktur i EU-CCMS
### Teknisk tillitsstruktur
[EU-CCMS](euccms.md) är den tekniska tillitsstrukturen för C-ITS i Europa och består av <mark>en gemensam europeisk policy och ledningsstruktur</mark> 
(CPA, TLM och ECTL), vilka styr en multipel Root CA-arkitektur med <mark>flera parallella Root CAs</mark>.

EU-CCMS är alltså en governance-styrd trust-list-modell – inte en klassisk single-root PKI-hierarki.

Den kryptografiska PKI-kedjan utgörs av Root CA, EA, AA och C-ITS-stationer.

Tilliten i systemet etableras genom att Root CAs listas i den europeiska trust-listan (ECTL), inte genom en överordnad europeisk super-root.

Följande komponenter utgör den faktiska kryptografiska tillitskedjan:
```
Root CA
   ↓
EA (Enrolment Authority)
   ↓
AA (Authorisation Authority)
   ↓
EC (Enrolment Credential)
   ↓
AT (Authorisation Ticket)
   ↓
C-ITS Station (OBU / RSU / Central ITS-station)
```

:one: **Root CA (RCA)**

- Utfärdar certifikat till EA och AA
- Är det kryptografiska tillitsankaret
- Flera Root CAs kan existera parallellt

:two: **Enrolment Authority (EA)**

- Utfärdar Enrollment Credentials (EC)
- Verifierar stationens identitet

:three: **Authorisation Authority (AA)**

- Utfärdar Authorization Tickets (AT)
- Ger rättigheter att använda specifika C-ITS-tjänster

:four: **C-ITS station**

OBU (fordon), RSU (vägkantsutrustning) eller central ITS-station, som:
- Signerar meddelanden med AT
- Validerar inkommande meddelanden via PKI-kedjan
<p>&nbsp;</p>

Följande delar är inte komponenter i den kryptografiska certifikatkedjan, men är avgörande för den PKI-kedjans tillitsmodell:

```
CPA (Certificate Policy Authority)
   ↓
TLM (Trust List Manager)
   ↓
ECTL (European Certificate Trust List)
   ↓
Godkända Root CAs
```

:one: **CPA – Certificate Policy Authority**

Policy-organ, som godkänner Root CAs, fastställer regelverk och övervakar efterlevnad.

CPA signerar inga C-ITS-certifikat.

:two: **TLM – Trust List Manager**

Publicerar och signerar ECTL. Lägger till/avlägsnar Root CAs i trust-listan. 

Är en central europeisk funktion, men inte en CA och utfärdar därmed inga EA/AA-certifikat.

:three: **ECTL – European Certificate Trust List**

En lista över alla godkända Root CAs (definierar vilka Root CAs som är betrodda).

ECTL distribueras till alla C-ITS stationer och är därmed det europeiska “tillitsankaret”.
<p>&nbsp;</p>

Detta innebär att:
- Alla root CAs är jämbördiga och inte underordnade en EU Root CA (multiple Root CA architecture)
- Tilliten baseras genom att de listas i ECTL
- En Root CA kan vara nationell, privat eller europeisk

```
                    ┌────────────────────────────┐
                    │        CPA (Policy)        │
                    └──────────────┬─────────────┘
                                   │
                    ┌──────────────▼─────────────┐
                    │            TLM             │
                    └──────────────┬─────────────┘
                                   │
                    ┌──────────────▼─────────────┐
                    │            ECTL            │
                    └──────────────┬─────────────┘
                                   │
        ┌──────────────────────────┼──────────────────────────┐
        │                          │                          │
  Root CA (EU)             Root CA (nation)             Root CA (OEM)
        │                          │                          │
        ▼                          ▼                          ▼
      EA / AA                   EA / AA                    EA / AA
        │                          │                          │
        ▼                          ▼                          ▼
      EC / AT                   EC / AT                    EC / AT
        │                          │                          │
        ▼                          ▼                          ▼
   C-ITS station             C-ITS station              C-ITS station
```

### Administrativ tillitsstruktur
Den administrativa tillitsstrukturen består av:
- Domänägare
- Registration Authority (RA)
- Policybeslut
- Roll- och behörighetsdefinition

<mark>Det är här nationell styrning sker</mark>.


:one: **C-ITS-domän**

En C-ITS-domän är en organisatorisk och policybaserad funktion (för en nationell eller organisatorisk miljö). Domänen ansvarar för registrering, certifikathantering och rollstyrning inom EU-CCMS.

En C-ITS-domän är en governance- och administrationsstruktur. Den är inte en Root CA och inte heller en teknisk komponent i den kryptografiska tillitskedjan.

> [!NOTE]
> Medan PKI-strukturen utgör den europeiska säkerhetsinfrastrukturen som gör att stationer kan lita på meddelanden från varandra, är en C-ITS-domän den organisatoriska miljön där C-ITS-enheter hanteras, till exempel inom ett land, en vägoperatör eller en tjänsteleverantör.
>
> Domänen ansvarar för att administrera sina egna enheter, ansluta dem till PKI-systemet och se till att de får de certifikat med korrekta rättigheter som krävs för att kunna kommunicera säkert. Domänen fungerar alltså som kopplingen mellan den lokala driften av C-ITS-system och den europeiska PKI-infrastrukturen.
>
> Se även [den övergripande strukturen för tillitsmodellen i EU-CCMS](euccms.md#%C3%B6vergripande-struktur).

:two: **C-ITS domänägare**

Domänägaren är en lednings- och styrningsfunktion ovanför RA.

Domänägaren:
* Fastställer policy och kan ändra reglerna
* Utser RA
* Utser de EA och AA, vilka kan konsumera data från domänens RA-system
* Beslutar om roll- och behörighetskategorier
* Beslutar om anslutningsvillkor
* Har incidentmandat
* Representerar Sverige i EU-CCMS

Domänägaren svarar på frågan:
> Hur ska svensk C-ITS-domän styras?

:three: **Registration Authority (RA)**

RA är den administrativa inträdespunkten och innehåller tillförlitliga uppgifter om:
- Aktörer
    - Organisationens identitet och juridisk form
    - Organisationsnummer
    - Kontaktpersoner
    - Status

- Stationer
    - Station-ID
    - Koppling till organisation
    - Stationstyp
    - Status

- Aktörernas representation genom betrodda C-ITS-stationer
    - Emergency vehicle
    - Public transport
    - Road operator
    - Behörighetsprofil

> [!NOTE]
> RA är en operativ, administrativ funktion, som:
>- Verifierar organisationer
>- Registrerar stationer
>- Kopplar station till organisation
>- Registrerar rollgrund
>- För in data i systemet
>- Dokumenterar beslut

RA fattar beslut inom ramen för C-ITS-domänens policy. 

RA är inte en kryptografisk roll i PKI-kedjan men är en kritisk säkerhetskontrollpunkt för de CA som utfärdar certifikat.

RA svarar på frågan:
> Är denna specifika organisation/station godkänd enligt reglerna?

:four: **Policybeslut**

När vi talar om policybeslut i C-ITS-sammanhang menar vi inte tekniska inställningar, utan formella beslut som styr:
- Vem som får delta i domänen?
- Under vilka villkor?
- Med vilka roller?
- Med vilket ansvar?
- Under vilka säkerhetskrav? 
- Hur incidenter ska hanteras? 
- Vem som får uteslutas?

Policybeslut i en domän ligger ovanför PKI-nivån och handlar inte om kryptografiska frågor.

> [!NOTE]
> Exempel på policybeslut i svensk kontext:
>- Ska alla kommuner få registrera RSU:er?
>- Ska privata väghållare få delta?
>- Vem avgör att ett fordon är `emergency vehicle`?
>- Ska kollektivtrafik ha prioritet i signaler?
>- Hur ska spärrning ske vid säkerhetsincident?
>- Ska utländska aktörer få registrera stationer i svensk domän?
>- Hur hanteras konflikt mellan kommun och stat vid rollfrågor?


:five: **Roll- och behörighetsdefinition**

Behörighet definierar vad en roll får göra i systemet. Det handlar exempelvis om:
- vilka meddelanden som får sändas.
- vilka attribut som får sättas.
- vilka funktioner som får användas.

EU definierar ramverket, men medlemsstater definierar tillämpningen. Det innebär att Sverige måste definiera:
- vilka roller som finns nationellt
- vilka organisationer som får dessa roller
- hur rollen verifieras

Domänägaren fastställer rollkatalog, behörighetsmodell och ansvarsfördelning.

RA registrerar organisationers roller samt stationers roller och vilken organisation de tillhör.

AA utfärdar sedan certifikat baserat på denna information.

Se även, [Roller och rättigheter i C-ITS](roles_in_cits.md)

## En möjlig vägval för svensk implementation
Tidigare avsnitt redogör för den europeiska tillitsmodellen, vilken etableras genom [EU-CCMS](euccms.md). Det är i grunden en modell som utgår från Europas mellanstatliga samarbetsstruktur där man vill värna om medlemsstaternas nationella suveränitet. EU sätter ramarna för det gemensamma europeiska säkerhetsramverket, men organiseringen av aktörer och ansvar i stor utsträckning sker på nationell nivå. 

Detta avsnitt redogör för hur en svensk C-ITS-domän kan etableras som ett organisatoriskt och avtalsmässigt ramverk för de aktörer som vill delta i C-ITS-systemet i Sverige.

### Rättsliga förutsättningar
Etableringen av en nationell struktur för C-ITS i Sverige innebär samverkan mellan ett stort antal aktörer från både offentlig och privat sektor, såsom myndigheter, kommuner och regioner, väghållare, fordonstillverkare, tjänsteleverantörer och operatörer. En reglering med ambition om att göra deltagande i C-ITS obligatoriskt eller i detalj styra ansvarsfördelning mellan aktörer kräver omfattande författningsändringar. Sådan lagstiftning skulle behöva omfatta bland annat frågor om:
- ansvar för drift av olika typer av C-ITS-stationer
- hantering av säkerhets- och certifikatinfrastruktur
- roller och ansvar mellan offentliga och privata aktörer
- tillsyn och efterlevnad
- förhållandet till kommunal självstyrelse och andra sektorsregelverk.

Lagstiftningsprocesser av detta slag bedöms inte vara realistiska, då de är omfattande och tidskrävande samt förutsätter utredning, remissförfarande och riksdagsbeslut. I många fall krävs även anpassningar till EU-rätten och befintlig nationell lagstiftning. Samtidigt är utvecklingen av C-ITS beroende av att samverkan mellan aktörer kan etableras i ett relativt tidigt skede för att möjliggöra teknisk utveckling, operativ erfarenhet och gradvis uppbyggnad av tjänster och marknader.

Mot denna bakgrund kan det vara ändamålsenligt att i ett inledande skede etablera den nationella C-ITS-strukturen genom avtalsbaserad anslutning. En sådan modell innebär att organisationer frivilligt kan ansluta sig till en gemensam domän genom att ingå avtal där de förbinder sig att följa gemensamma regler för säkerhet, interoperabilitet och ansvar.

En avtalsbaserad modell möjliggör att:
- aktörer kan börja samverka utan att ny lagstiftning behöver inväntas (Detta utesluter dock inte att myndigheter kan behöva särskilda uppdrag eller justerade regleringsbrev),
- tekniska och organisatoriska lösningar kan utvecklas och prövas i praktiken
- erfarenheter kan samlas inför eventuella framtida regulatoriska åtgärder.

En sådan utveckling är inte ovanlig vid etablering av ny digital infrastruktur. I flera fall har frivilliga samverkansmodeller och avtalsbaserade strukturer etablerats först, medan lagstiftning och mer formaliserade regleringar senare har utvecklats i takt med att användningen ökar och behovet av rättslig tydlighet blir större.

Utgångspunkten för den svenska C-ITS-domänen är därför att deltagande i ett första skede sker genom avtalad anslutning till ett gemensamt tillits- och säkerhetsramverk, inom ramen för EU:s C-ITS-arkitektur och EU-CCMS.

### Principer för svensk C-ITS-domän

#### Öppen men reglerad anslutning
Organisationer ska kunna ansluta sina C-ITS-stationer och tjänster till domänen om de uppfyller de krav som gäller för interoperabilitet, säkerhet och ansvar.

Anslutning sker genom avtal där organisationen förbinder sig att följa:
- EU:s C-ITS-policyer
- ETSI-standarder
- nationella (domänens) policyer för roller och ansvar.

#### Aktörernas rådighet över sina system
Varje organisation behåller rådighet över sina:
- C-ITS-stationer,
- tjänster,
- leverantörer,
- interna system.

Den svenska C-ITS-domänen ska därför inte vara en central teknisk plattform utan ett federativt ramverk som möjliggör samverkan mellan självständiga aktörer.

#### Gemensamma säkerhetsregler
Alla aktörer i domänen ska följa EU-CCMS tillitsmodell och säkerhetspolicy.

C-ITS är ett distribuerat system där många organisationer behandlar delar av systemets data, vilket innebär att informationssäkerheten är ett gemensamt ansvar mellan aktörerna – och behöver regleras i det federativa ramverket. 

#### Interoperabilitet och standardisering
Domänen ska säkerställa att aktörer använder harmoniserade standarder och specifikationer för:
- meddelandeformat,
- certifikathantering,
- säkerhetsfunktioner,
- kommunikationsprotokoll.

Detta möjliggör interoperabilitet mellan aktörer i Sverige och övriga Europa.

#### Möjlighet till konkurrens och innovation
Domänmodellen ska inte begränsa marknaden till enskilda leverantörer eller tekniska lösningar.

Aktörer ska kunna välja leverantörer för exempelvis:
- C-ITS-stationer
- PKI-tjänster
- backend-system
- tjänsteplattformar.

På så sätt kan innovation och konkurrens utvecklas inom ramen för ett gemensamt tillitsramverk.

### Roller i domänen
För att möjliggöra samverkan behövs tydliga roller.

#### Domänägare
Den organisation som ansvarar för:
- nationell policy
- anslutningsregler
- samordning med EU-CCMS
- representation i europeiska forum.

Domänägaren ansvarar för styrningen av domänen men behöver inte driva operativa system.

#### Registration Authority (RA)
RA ansvarar för att:
- identifiera och registrera C-ITS-stationer
- verifiera organisationer
- godkänna anslutning till EU-CCMS.

RA fungerar därmed som den organisatoriska kopplingen mellan nationella aktörer och det europeiska certifikatsystemet.

#### C-ITS-station operatörer
Organisationer som driver C-ITS-stationer, exempelvis:
- väghållare
- kommuner
- tillverkare och leverantörer av stationer

Dessa ansvarar för att stationerna uppfyller de tekniska och säkerhetsmässiga kraven.

#### Tjänsteleverantörer
Organisationer som utvecklar och tillhandahåller C-ITS-tjänster till användare eller andra aktörer.

#### Säkerhets- och certifikataktörer
Aktörer inom EU-CCMS-strukturen, såsom utfärdare (EA/AA) som är godkända för domänen.

### Avtal (och vid behov granskning) för anslutning
Anslutning till den svenska C-ITS-domänen sker genom ett anslutningsavtal mellan domänägaren och den organisation som vill ansluta sina stationer. I vissa fall kan avtal inbegripa någon form av tillitsgranskning.

Avtalet reglerar bland annat:
- ansvar för C-ITS-stationer
- efterlevnad av säkerhetspolicy
- användning av certifikat
- incidenthantering
- loggning och revision.

Genom denna modell kan organisationer ansluta sig till domänen utan att ge upp kontrollen över sina egna stationer och system, samtidigt som säkerhet och interoperabilitet kan upprätthållas.

### Relation till EU-CCMS
Den svenska C-ITS-domänen utgör ett nationellt organisatoriskt lager ovanpå EU-CCMS PKI.

Den europeiska nivån ansvarar för:
- den europeiska tillitsmodellen
- rotcertifikat och certifikathierarki
- gemensamma säkerhetspolicyer.

Den svenska domänen ansvarar för:
- vilka aktörer som deltar i den nationella C-ITS-miljön
- hur dessa ansluts till EU-CCMS
- nationella roller och ansvar.

På så sätt kombineras europeisk säkerhet och interoperabilitet med nationell styrning.

### Hur hänger det ihop i praktiken
En balanserad modell skulle kunna vara enligt följande:
- Regeringen ger ett övergripande uppdrag
- Trafikverket i samarbete med Transportstyrelsen och PTS etablerar en nationell C-ITS-domän
- RA utpekas och etablerar ett centralt RA-verksamhetssystem där registreringsrätt kan delegeras lokalt
- Offentliga organisationer ansluts genom avtal
- Privata aktörer ansluts genom avtal där tillitsgranskning är ett krav för anslutning

### Risker
Det föreslagna angreppssättet medför fördelar som kan bidra till att förenkla och effektivisera ett införande i det skede där Sverige, och implementeringen av C-ITS i Europa i stort, för närvarande befinner sig.

På längre sikt, i ett scenario där C-ITS utvecklas till en samhällskritisk funktion, finns det emellertid risker som behöver beaktas:
- Vissa aktörer, t ex en kommun eller region kan välja att inte ansluta
- Alternativa RA-strukturer kan uppstå
- Otydlig rådighet i kris
- Ojämn täckning nationellt

Om C-ITS blir samhällskritiskt kan principen om frivillighet bli en svaghet. I ett sådant läge kan det därför uppstå behov av att lagstiftning och författningsreglering utvecklas för att säkerställa en mer sammanhållen nationell styrning.


### Domänstrukturer – alternativa modeller

#### En nationell domän
text...

#### Sektorsdomäner
text...

#### Domän per kommun/region
text...

### RA-struktur – Central vs Federerad
text...

### Offentlig vs Privat domänägare
text...






<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  





