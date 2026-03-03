# Möjlig svensk alternativ
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
<p>/nbsp;</p>

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




EU-CCMS består av:
- EU Root CA (gemensamt europeiskt tillitsankare)
- Enrollment Authority (EA)
- Authorization Authority (AA)
- C-ITS-stationer (OBU, RSU, Central ITS-S)

Endast Root CA, EA, AA och stationer är delar av PKI-kedjan.
Detta utgör den <mark>övergripande europeiska tillismodellen</mark>.

Varje medlemsstat (eller flera medlemsstater) kan ha en <mark>egen underordnad Root CA</mark>, som:
- är certifierad (cross-certified eller underordnad) via EU Root
- driver eller delegerar till underordnade certifikatutfärdare
- hanterar certifikaten för underliggande EA/AA

En nationell (eller regional) Root-CA är inte fristående tillitsankare och är underordnade EU Root CA inom EU-CCMS-tillitsmodellen.

```
EU Root CA
   ↓
Root CA (per medlemsstat/region)
   ↓
EA / AA
   ↓
EC / AT (stationer)
```

2.2 Administrativ struktur

Utanför PKI-kedjan ligger:

Registration Authority (RA)

Domänägare (governance)

Policybeslut

Roll- och behörighetsdefinition

Det är här nationell styrning sker.
