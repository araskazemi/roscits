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
<p>&nbsp;</p>

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
  Root CA (SE)              Root CA (FR)               Root CA (Privat)
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

En C-ITS-domän är en organisatorisk och policybaserad funktion som ansvarar för registrering, certifikathantering och rollstyrning inom EU-CCMS.

En C-ITS-domän är en governance-struktur. Den är inte en Root CA och inte heller en teknisk komponent i den kryptografiska tillitskedjan.


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
text...

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








